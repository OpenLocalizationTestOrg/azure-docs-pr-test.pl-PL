---
title: "Samouczek: Integracji Azure Active Directory z wysłannika | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i wysłannika."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 49211b35ab3e28e0df914061e7fa623907935638
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="8ec3a-103">Samouczek: Integracji Azure Active Directory z wysłannika</span><span class="sxs-lookup"><span data-stu-id="8ec3a-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="8ec3a-104">Z tego samouczka dowiesz się integrowanie wysłannika w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ec3a-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ec3a-105">Integracja z usługą Azure AD wysłannika zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8ec3a-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8ec3a-106">Można kontrolować w usłudze Azure AD, który ma dostęp do wysłannika.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="8ec3a-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do wysłannika (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8ec3a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8ec3a-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ec3a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ec3a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ec3a-110">Prerequisites</span></span>

<span data-ttu-id="8ec3a-111">Aby skonfigurować integrację usługi Azure AD z wysłannika, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8ec3a-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="8ec3a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ec3a-113">Wysłannika logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8ec3a-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ec3a-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ec3a-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8ec3a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ec3a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ec3a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ec3a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ec3a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8ec3a-118">Scenario description</span></span>
<span data-ttu-id="8ec3a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ec3a-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8ec3a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ec3a-121">Dodawanie wysłannika z galerii</span><span class="sxs-lookup"><span data-stu-id="8ec3a-121">Adding Envoy from the gallery</span></span>
2. <span data-ttu-id="8ec3a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ec3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="8ec3a-123">Dodawanie wysłannika z galerii</span><span class="sxs-lookup"><span data-stu-id="8ec3a-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="8ec3a-124">Aby skonfigurować integrację wysłannika do usługi Azure AD, należy dodać wysłannika z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8ec3a-125">**Aby dodać wysłannika z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ec3a-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec3a-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="8ec3a-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8ec3a-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="8ec3a-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="8ec3a-133">W polu wyszukiwania wpisz **wysłannika**, wybierz pozycję **wysłannika** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![Wysłannika na liście wyników](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8ec3a-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ec3a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8ec3a-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z wysłannika w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ec3a-137">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w wysłannika dla użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="8ec3a-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w wysłannika musi się.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="8ec3a-139">W wysłannika, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8ec3a-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z wysłannika, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="8ec3a-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8ec3a-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8ec3a-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ec3a-143">**[Tworzenie użytkownika testowego wysłannika](#create-an-envoy-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta wysłannika połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ec3a-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ec3a-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8ec3a-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ec3a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8ec3a-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji wysłannika.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="8ec3a-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z wysłannika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ec3a-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec3a-149">W portalu Azure na **wysłannika** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="8ec3a-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="8ec3a-153">Na **wysłannika domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8ec3a-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny wysłannika pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="8ec3a-155">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="8ec3a-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="8ec3a-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-156">This value is not real.</span></span> <span data-ttu-id="8ec3a-157">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="8ec3a-158">Skontaktuj się z [zespołem pomocy technicznej klienta wysłannika](https://envoy.com/contact/) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

4. <span data-ttu-id="8ec3a-159">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="8ec3a-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8ec3a-163">Na **konfiguracji wysłannika** , kliknij przycisk **skonfigurować wysłannika** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8ec3a-164">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8ec3a-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja wysłannika](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="8ec3a-166">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy wysłannika jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="8ec3a-167">Na pasku narzędzi u góry kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="8ec3a-168">![Wysłannika](./media/active-directory-saas-envoy-tutorial/ic776782.png "wysłannika")</span><span class="sxs-lookup"><span data-stu-id="8ec3a-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="8ec3a-169">Kliknij przycisk **firmy**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-169">Click **Company**.</span></span>

    <span data-ttu-id="8ec3a-170">![Firmy](./media/active-directory-saas-envoy-tutorial/ic776783.png "firmy")</span><span class="sxs-lookup"><span data-stu-id="8ec3a-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="8ec3a-171">Kliknij przycisk **SAML**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-171">Click **SAML**.</span></span>

    <span data-ttu-id="8ec3a-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="8ec3a-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="8ec3a-173">W **uwierzytelnianie SAML** konfiguracji sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8ec3a-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="8ec3a-174">![Uwierzytelnianie SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="8ec3a-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="8ec3a-175">Wartość HQ identyfikator lokalizacji jest automatycznie generowane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="8ec3a-176">a.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-176">a.</span></span> <span data-ttu-id="8ec3a-177">W **odcisk palca** pole tekstowe, Wklej **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="8ec3a-178">b.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-178">b.</span></span> <span data-ttu-id="8ec3a-179">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana tworzą portalu Azure do **URL SAML HTTP dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="8ec3a-180">c.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-180">c.</span></span> <span data-ttu-id="8ec3a-181">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="8ec3a-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="8ec3a-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8ec3a-183">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8ec3a-184">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ec3a-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8ec3a-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec3a-185">Create an Azure AD test user</span></span>

<span data-ttu-id="8ec3a-186">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="8ec3a-188">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ec3a-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec3a-189">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8ec3a-191">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8ec3a-193">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8ec3a-195">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8ec3a-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8ec3a-197">a.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-197">a.</span></span> <span data-ttu-id="8ec3a-198">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ec3a-199">b.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-199">b.</span></span> <span data-ttu-id="8ec3a-200">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8ec3a-201">c.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-201">c.</span></span> <span data-ttu-id="8ec3a-202">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8ec3a-203">d.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-203">d.</span></span> <span data-ttu-id="8ec3a-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="8ec3a-205">Tworzenie użytkownika testowego wysłannika</span><span class="sxs-lookup"><span data-stu-id="8ec3a-205">Create an Envoy test user</span></span>

<span data-ttu-id="8ec3a-206">Nie ma elementu akcji do skonfigurowania inicjowania obsługi administracyjnej wysłannika użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="8ec3a-207">Gdy przypisany użytkownik próbuje zalogować się przy użyciu panelu dostępu wysłannika, wysłannika sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="8ec3a-208">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez wysłannika.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8ec3a-209">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec3a-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="8ec3a-210">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu wysłannika.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="8ec3a-212">**Aby przypisać Simona Britta wysłannika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ec3a-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec3a-213">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8ec3a-215">Na liście aplikacji zaznacz **wysłannika**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-215">In the applications list, select **Envoy**.</span></span>

    ![Łącze wysłannika na liście aplikacji](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="8ec3a-217">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="8ec3a-219">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-219">Click **Add** button.</span></span> <span data-ttu-id="8ec3a-220">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="8ec3a-222">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8ec3a-223">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ec3a-224">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8ec3a-225">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ec3a-225">Test single sign-on</span></span>

<span data-ttu-id="8ec3a-226">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8ec3a-227">Po kliknięciu kafelka wysłannika w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji wysłannika.</span><span class="sxs-lookup"><span data-stu-id="8ec3a-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="8ec3a-228">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ec3a-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8ec3a-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8ec3a-229">Additional resources</span></span>

* [<span data-ttu-id="8ec3a-230">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ec3a-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ec3a-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ec3a-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

