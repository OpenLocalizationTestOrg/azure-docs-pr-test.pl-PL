---
title: "Samouczek: Integracji Azure Active Directory z usług sieci Web firmy Amazon (AWS) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usług sieci Web firmy Amazon (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="b1e8e-103">Samouczek: Integracji Azure Active Directory z usług sieci Web firmy Amazon (AWS)</span><span class="sxs-lookup"><span data-stu-id="b1e8e-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="b1e8e-104">Z tego samouczka, dowiesz się, jak toointegrate Amazon usług sieci Web (AWS) z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1e8e-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1e8e-105">Integrowanie usługi Amazon Web Services (AWS) z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b1e8e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooAmazon usług sieci Web (AWS)</span><span class="sxs-lookup"><span data-stu-id="b1e8e-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="b1e8e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAmazon usług sieci Web (AWS) (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e8e-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1e8e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b1e8e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b1e8e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1e8e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="b1e8e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b1e8e-110">Prerequisites</span></span>

<span data-ttu-id="b1e8e-111">tooconfigure integracji z usługą Azure AD z Amazon Web Services (AWS), należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="b1e8e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e8e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1e8e-113">Amazon Web Services (AWS) jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b1e8e-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1e8e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1e8e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1e8e-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b1e8e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1e8e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1e8e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b1e8e-118">Scenario description</span></span>
<span data-ttu-id="b1e8e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1e8e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1e8e-121">Dodawanie Amazon Web Services (AWS) z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b1e8e-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="b1e8e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b1e8e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="b1e8e-123">Dodawanie Amazon Web Services (AWS) z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b1e8e-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="b1e8e-124">tooconfigure hello integracji z usługami sieci Web Amazon (AWS) do usługi Azure AD, należy tooadd Amazon Web Services (AWS) z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b1e8e-125">**tooadd Amazon usług sieci Web (AWS) z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b1e8e-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1e8e-126">W hello  **[Azure Portal](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b1e8e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b1e8e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b1e8e-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b1e8e-133">W polu wyszukiwania hello wpisz **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="b1e8e-135">W panelu wyników hello, wybierz **Amazon Web Services (AWS)**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1e8e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b1e8e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b1e8e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Amazon Web usługi (AWS) w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1e8e-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Amazon Web Services (AWS) jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="b1e8e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Amazon Web Services (AWS) musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="b1e8e-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="b1e8e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="b1e8e-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Amazon Web Services (AWS), należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b1e8e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b1e8e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1e8e-145">**[Tworzenie użytkownika testowego usług Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave odpowiednikiem Simona Britta w Amazon usług sieci Web (AWS), będącego jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="b1e8e-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1e8e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1e8e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b1e8e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1e8e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji usługi sieci Web firmy Amazon (AWS).</span><span class="sxs-lookup"><span data-stu-id="b1e8e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="b1e8e-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Amazon usług sieci Web (AWS) wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b1e8e-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="b1e8e-151">W hello portalu Azure na powitania **Amazon Web Services (AWS)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b1e8e-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="b1e8e-155">Na powitania **Amazon Web Services (AWS) domeny i adres URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="b1e8e-157">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="b1e8e-159">Witaj Amazon Web Services (AWS) aplikacji oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b1e8e-160">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="b1e8e-161">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="b1e8e-162">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-162">hello following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="b1e8e-164">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="b1e8e-165">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="b1e8e-165">Attribute Name</span></span>  | <span data-ttu-id="b1e8e-166">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="b1e8e-166">Attribute Value</span></span> | <span data-ttu-id="b1e8e-167">przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="b1e8e-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="b1e8e-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="b1e8e-168">RoleSessionName</span></span> | <span data-ttu-id="b1e8e-169">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b1e8e-169">user.userprincipalname</span></span> | <span data-ttu-id="b1e8e-170">https://awS.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="b1e8e-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="b1e8e-171">Rola</span><span class="sxs-lookup"><span data-stu-id="b1e8e-171">Role</span></span>            | <span data-ttu-id="b1e8e-172">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="b1e8e-172">user.assignedroles</span></span> |  <span data-ttu-id="b1e8e-173">https://awS.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="b1e8e-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="b1e8e-174">Należy użytkownika hello tooconfigure inicjowania obsługi usługi Azure AD toofetch wszystkie role hello z konsoli usług AWS.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="b1e8e-175">Można znaleźć hello inicjowania obsługi administracyjnej poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="b1e8e-176">a.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-176">a.</span></span> <span data-ttu-id="b1e8e-177">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="b1e8e-179">b.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-179">b.</span></span> <span data-ttu-id="b1e8e-180">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b1e8e-182">c.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-182">c.</span></span> <span data-ttu-id="b1e8e-183">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="b1e8e-184">Dodaj wartość Namespace hello podane powyżej.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="b1e8e-185">d.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-185">d.</span></span> <span data-ttu-id="b1e8e-186">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-186">Click **Ok**.</span></span>

7. <span data-ttu-id="b1e8e-187">Kliknij przycisk **zapisać** przycisk ustawień hello toosave na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b1e8e-189">W oknie innej przeglądarki, witryny firmy Amazon Web Services (AWS) tooyour logowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="b1e8e-190">Kliknij przycisk **konsoli głównej**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-190">Click **Console Home**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][11]

10. <span data-ttu-id="b1e8e-192">Kliknij przycisk **IAM** z **zabezpieczeń, tożsamości i zgodności** usługi.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][12]

11. <span data-ttu-id="b1e8e-194">Kliknij przycisk **dostawców tożsamości**, a następnie kliknij przycisk **Tworzenie dostawcy**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][13]

12. <span data-ttu-id="b1e8e-196">Na powitania **Konfigurowanie dostawcy** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][14]
 
    <span data-ttu-id="b1e8e-198">a.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-198">a.</span></span> <span data-ttu-id="b1e8e-199">Jako **typ dostawcy**, wybierz pozycję **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="b1e8e-200">b.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-200">b.</span></span> <span data-ttu-id="b1e8e-201">W hello **Nazwa dostawcy** tekstowym, wpisz nazwę dostawcy (np.: *drewna*).</span><span class="sxs-lookup"><span data-stu-id="b1e8e-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="b1e8e-202">c.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-202">c.</span></span> <span data-ttu-id="b1e8e-203">tooupload pliku metadanych pobranych, kliknij przycisk **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="b1e8e-204">d.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-204">d.</span></span> <span data-ttu-id="b1e8e-205">Kliknij przycisk **następny krok**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="b1e8e-206">Na powitania **Sprawdź informacje o dostawcy** strony okna dialogowego, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej][15]

14. <span data-ttu-id="b1e8e-208">Kliknij przycisk **ról**, a następnie kliknij przycisk **Utwórz nową rolę**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej][16]

15. <span data-ttu-id="b1e8e-210">Na powitania **Ustaw nazwę roli** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej][17] 

    <span data-ttu-id="b1e8e-212">a.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-212">a.</span></span> <span data-ttu-id="b1e8e-213">W hello **nazwy roli** tekstowym, wpisz nazwę roli (np.: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="b1e8e-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="b1e8e-214">b.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-214">b.</span></span> <span data-ttu-id="b1e8e-215">Kliknij przycisk **następny krok**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="b1e8e-216">Na powitania **wybierz typ roli** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej][18] 

    <span data-ttu-id="b1e8e-218">a.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-218">a.</span></span> <span data-ttu-id="b1e8e-219">Wybierz **roli dostęp dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="b1e8e-220">b.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-220">b.</span></span> <span data-ttu-id="b1e8e-221">W hello **Grant sieci Web rejestracji jednokrotnej (WebSSO) dostępu tooSAML dostawców** kliknij **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="b1e8e-222">Na powitania **ustanowić zaufanie** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej][19] 

    <span data-ttu-id="b1e8e-224">a.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-224">a.</span></span> <span data-ttu-id="b1e8e-225">Jako dostawca SAML wybierz hello SAML dostawcy utworzonym wcześniej (np.: *drewna*)</span><span class="sxs-lookup"><span data-stu-id="b1e8e-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="b1e8e-226">b.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-226">b.</span></span> <span data-ttu-id="b1e8e-227">Kliknij przycisk **następny krok**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="b1e8e-228">Na powitania **Sprawdź zaufania roli** okna dialogowego, kliknij przycisk **następnego kroku**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej][32]

19. <span data-ttu-id="b1e8e-230">Na powitania **Dołącz zasady** okna dialogowego, kliknij przycisk **następnego kroku**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej][33]

20. <span data-ttu-id="b1e8e-232">Na powitania **przeglądu** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej][34]
 
    <span data-ttu-id="b1e8e-234">a.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-234">a.</span></span> <span data-ttu-id="b1e8e-235">Kliknij przycisk **utworzyć rolę**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-235">Click **Create Role**.</span></span>

    <span data-ttu-id="b1e8e-236">b.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-236">b.</span></span> <span data-ttu-id="b1e8e-237">Tworzenie ról tyle zgodnie z potrzebami i zamapowania ich toohello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="b1e8e-238">Teraz skonfigurować użytkownika hello inicjowania obsługi administracyjnej toofetch wszystkie role hello z usług AWS</span><span class="sxs-lookup"><span data-stu-id="b1e8e-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="b1e8e-239">a.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-239">a.</span></span> <span data-ttu-id="b1e8e-240">Podczas logowania konsoli usług AWS hello przy użyciu konta głównego</span><span class="sxs-lookup"><span data-stu-id="b1e8e-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="b1e8e-241">b.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-241">b.</span></span> <span data-ttu-id="b1e8e-242">W hello prawym górnym rogu kliknij swoją nazwę, a następnie kliknij przycisk hello **moje poświadczenia zabezpieczeń** opcji.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="b1e8e-243">Spowoduje to otwarcie ekranu jako komunikat ostrzegawczy.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="b1e8e-244">Kliknij przycisk hello **poświadczenia zabezpieczeń** toopass przycisk hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![Konfigurowanie rejestracji jednokrotnej][36]

       ![Konfigurowanie rejestracji jednokrotnej][37]

    <span data-ttu-id="b1e8e-247">c.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-247">c.</span></span> <span data-ttu-id="b1e8e-248">W hello kluczy dostępu do sekcji kliknij hello **Utwórz nowy klucz dostępu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="b1e8e-249">Spowoduje to wygenerowanie hello identyfikator klucza dostępu i wartość tokenu.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![Konfigurowanie rejestracji jednokrotnej][38]

    <span data-ttu-id="b1e8e-251">d.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-251">d.</span></span> <span data-ttu-id="b1e8e-252">Skopiuj obie te wartości i go również pobrać, tak aby nie zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="b1e8e-253">e.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-253">e.</span></span> <span data-ttu-id="b1e8e-254">W hello portalu Azure na stronie integracji aplikacji hello, Amazon Web Services (AWS), kliknij przycisk **inicjowania obsługi administracyjnej**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Konfigurowanie rejestracji jednokrotnej][35]

    <span data-ttu-id="b1e8e-256">f.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-256">f.</span></span> <span data-ttu-id="b1e8e-257">Ustaw tryb inicjowania obsługi administracyjnej hello zbyt**automatyczne**</span><span class="sxs-lookup"><span data-stu-id="b1e8e-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![Konfigurowanie rejestracji jednokrotnej][39]

    <span data-ttu-id="b1e8e-259">g.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-259">g.</span></span> <span data-ttu-id="b1e8e-260">Teraz w hello **clientsecret** i **klucz tajny tokenu** Wklej hello odpowiednie wartości, które zostały skopiowane z konsoli usług AWS.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="b1e8e-261">h.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-261">h.</span></span> <span data-ttu-id="b1e8e-262">Możesz kliknąć hello **Testuj połączenie** przycisku łączności hello tootest.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="b1e8e-263">Gdy zostanie pomyślnie przesłany można uruchomić hello inicjowania obsługi administracyjnej łącznika.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![Konfigurowanie rejestracji jednokrotnej][40]

    <span data-ttu-id="b1e8e-265">i.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-265">i.</span></span> <span data-ttu-id="b1e8e-266">Teraz Włącz hello stan inicjowania obsługi administracyjnej za**na**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="b1e8e-267">Spowoduje to uruchomienie pobierania hello ról z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-267">This starts fetching hello roles from hello application.</span></span>

       ![Konfigurowanie rejestracji jednokrotnej][41]

    > [!NOTE]
    > <span data-ttu-id="b1e8e-269">Azure działa Usługa AD inicjowania obsługi administracyjnej co po niektóre role hello toosync czasu z usług AWS.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="b1e8e-270">Powinny zostać wyświetlone wszystkie hello dostawcy tożsamości dołączony ról usług AWS z usługą Azure AD i można było ich użyć podczas przypisywania toousers aplikacji hello lub grup.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1e8e-271">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e8e-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="b1e8e-272">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b1e8e-274">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b1e8e-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1e8e-275">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1e8e-277">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1e8e-279">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1e8e-281">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1e8e-283">a.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-283">a.</span></span> <span data-ttu-id="b1e8e-284">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1e8e-285">b.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-285">b.</span></span> <span data-ttu-id="b1e8e-286">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1e8e-287">c.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-287">c.</span></span> <span data-ttu-id="b1e8e-288">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b1e8e-289">d.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-289">d.</span></span> <span data-ttu-id="b1e8e-290">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="b1e8e-291">Tworzenie użytkownika testowego usług Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="b1e8e-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="b1e8e-292">W kolejności tooenable usługi Azure AD użytkownicy toolog w tooAmazon usług sieci Web (AWS) są udostępniane do usług sieci Web firmy Amazon (AWS).</span><span class="sxs-lookup"><span data-stu-id="b1e8e-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="b1e8e-293">W przypadku hello z usług sieci Web firmy Amazon (AWS) Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="b1e8e-294">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b1e8e-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1e8e-295">Zaloguj się za tooyour **Amazon Web Services (AWS)** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="b1e8e-296">Kliknij przycisk hello **konsoli głównej** ikony.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-296">Click hello **Console Home** icon.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][11]

3. <span data-ttu-id="b1e8e-298">Tożsamość i zarządzanie dostępem.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-298">Click Identity and Access Management.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][28]

4. <span data-ttu-id="b1e8e-300">W hello pulpitu nawigacyjnego, kliknij przycisk **użytkowników**, a następnie kliknij przycisk **Utwórz nowych użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][29]

5. <span data-ttu-id="b1e8e-302">W oknie dialogowym Tworzenie użytkownika hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b1e8e-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][30]   
    
    <span data-ttu-id="b1e8e-304">a.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-304">a.</span></span> <span data-ttu-id="b1e8e-305">W hello **wprowadź nazwy użytkowników** pól tekstowych, wpisz nazwę użytkownika Simona Brita (userprincipalname) w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="b1e8e-306">b.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-306">b.</span></span> <span data-ttu-id="b1e8e-307">Kliknij przycisk **utworzyć.**</span><span class="sxs-lookup"><span data-stu-id="b1e8e-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b1e8e-308">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e8e-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b1e8e-309">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooAmazon dostęp do usług sieci Web (AWS).</span><span class="sxs-lookup"><span data-stu-id="b1e8e-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b1e8e-311">**tooassign tooAmazon Simona Britta usług sieci Web (AWS) wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b1e8e-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="b1e8e-312">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b1e8e-314">Z listy aplikacji hello wybierz **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="b1e8e-316">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b1e8e-318">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-318">Click **Add** button.</span></span> <span data-ttu-id="b1e8e-319">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b1e8e-321">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b1e8e-322">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1e8e-323">Na **wybierz rolę** kartę, hello wybierz odpowiednią rolę dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="b1e8e-324">Te role są wyświetlane z nazwą roli hello i nazwa dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="b1e8e-325">Dzięki temu można łatwo zidentyfikować hello role z usług AWS.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="b1e8e-326">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b1e8e-327">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b1e8e-327">Testing single sign-on</span></span>

<span data-ttu-id="b1e8e-328">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b1e8e-329">Po kliknięciu powitalne Amazon Web Services (AWS) kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Amazon Web Services (AWS) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1e8e-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b1e8e-330">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b1e8e-330">Additional resources</span></span>

* [<span data-ttu-id="b1e8e-331">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1e8e-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1e8e-332">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b1e8e-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
