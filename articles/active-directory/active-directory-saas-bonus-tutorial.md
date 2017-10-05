---
title: 'Samouczek: Integracji Azure Active Directory z Bonusly | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 29a88b2efdb9f0f33f7933bc654a5a0fdf589c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="bd44f-103">Samouczek: Integracji Azure Active Directory z Bonusly</span><span class="sxs-lookup"><span data-stu-id="bd44f-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="bd44f-104">Z tego samouczka dowiesz się integrowanie Bonusly z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd44f-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd44f-105">Integracja z usługą Azure AD Bonusly zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bd44f-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bd44f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Bonusly</span><span class="sxs-lookup"><span data-stu-id="bd44f-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="bd44f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Bonusly (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44f-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd44f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bd44f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bd44f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd44f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd44f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bd44f-110">Prerequisites</span></span>

<span data-ttu-id="bd44f-111">Aby skonfigurować integrację usługi Azure AD z Bonusly, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bd44f-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="bd44f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd44f-113">Bonusly logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bd44f-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd44f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bd44f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd44f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bd44f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd44f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bd44f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd44f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd44f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd44f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bd44f-118">Scenario description</span></span>
<span data-ttu-id="bd44f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bd44f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd44f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bd44f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd44f-121">Dodawanie Bonusly z galerii</span><span class="sxs-lookup"><span data-stu-id="bd44f-121">Adding Bonusly from the gallery</span></span>
2. <span data-ttu-id="bd44f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bd44f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="bd44f-123">Dodawanie Bonusly z galerii</span><span class="sxs-lookup"><span data-stu-id="bd44f-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="bd44f-124">Aby skonfigurować integrację usługi Azure AD Bonusly, należy dodać Bonusly z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bd44f-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bd44f-125">**Aby dodać Bonusly z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bd44f-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bd44f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bd44f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="bd44f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bd44f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="bd44f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd44f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="bd44f-133">W polu wyszukiwania wpisz **Bonusly**, wybierz pozycję **Bonusly** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bd44f-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span></span>

    ![Bonusly na liście wyników](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bd44f-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bd44f-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="bd44f-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Bonusly w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="bd44f-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd44f-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Bonusly jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd44f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="bd44f-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Bonusly musi się.</span><span class="sxs-lookup"><span data-stu-id="bd44f-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="bd44f-139">W Bonusly, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="bd44f-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bd44f-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Bonusly, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="bd44f-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bd44f-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bd44f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bd44f-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bd44f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd44f-143">**[Tworzenie użytkownika testowego Bonusly](#create-a-bonusly-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Bonusly połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd44f-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd44f-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bd44f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd44f-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="bd44f-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bd44f-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bd44f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bd44f-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w Bonusly aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd44f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="bd44f-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Bonusly, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bd44f-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="bd44f-149">W portalu Azure na **Bonusly** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bd44f-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="bd44f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="bd44f-153">Na **Bonusly domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bd44f-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny bonusly pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="bd44f-155">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="bd44f-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd44f-156">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bd44f-156">The value is not real.</span></span> <span data-ttu-id="bd44f-157">Zaktualizuj tę wartość do rzeczywistego adresu URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="bd44f-157">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="bd44f-158">Skontaktuj się z [zespołem pomocy technicznej Bonusly](https://Bonusly/contact) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="bd44f-158">Contact [Bonusly support team](https://Bonusly/contact) to get the value.</span></span>
 
4. <span data-ttu-id="bd44f-159">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="bd44f-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="bd44f-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bd44f-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bd44f-163">Na **Bonusly konfiguracji** kliknij **skonfigurować Bonusly** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bd44f-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bd44f-164">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bd44f-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Bonusly konfiguracji](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="bd44f-166">W oknie innej przeglądarki, zaloguj się do Twojego **Bonusly** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="bd44f-166">In a different browser window, log in to your **Bonusly** tenant.</span></span>

8. <span data-ttu-id="bd44f-167">Na pasku narzędzi u góry kliknij **ustawienia**, a następnie wybierz **integracji i aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="bd44f-168">![Sekcja społecznościowych bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="bd44f-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="bd44f-169">W obszarze **rejestracji jednokrotnej**, wybierz pozycję **SAML**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="bd44f-170">Na **SAML** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bd44f-170">On the **SAML** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="bd44f-171">![Strony okna dialogowego Saml bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="bd44f-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="bd44f-172">a.</span><span class="sxs-lookup"><span data-stu-id="bd44f-172">a.</span></span> <span data-ttu-id="bd44f-173">W **logowania jednokrotnego IdP docelowy adres URL** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bd44f-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="bd44f-174">b.</span><span class="sxs-lookup"><span data-stu-id="bd44f-174">b.</span></span> <span data-ttu-id="bd44f-175">W **wystawcy IdP** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bd44f-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="bd44f-176">c.</span><span class="sxs-lookup"><span data-stu-id="bd44f-176">c.</span></span> <span data-ttu-id="bd44f-177">W **adres URL logowania IdP** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bd44f-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bd44f-178">d.</span><span class="sxs-lookup"><span data-stu-id="bd44f-178">d.</span></span> <span data-ttu-id="bd44f-179">Wklej **odcisk palca** wartość skopiowany z portalu Azure do **odcisk palca certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="bd44f-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="bd44f-180">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="bd44f-181">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="bd44f-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bd44f-182">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="bd44f-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bd44f-183">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd44f-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bd44f-184">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44f-184">Create an Azure AD test user</span></span>
<span data-ttu-id="bd44f-185">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bd44f-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="bd44f-187">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bd44f-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bd44f-188">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bd44f-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd44f-190">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd44f-192">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd44f-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd44f-194">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bd44f-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd44f-196">a.</span><span class="sxs-lookup"><span data-stu-id="bd44f-196">a.</span></span> <span data-ttu-id="bd44f-197">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd44f-198">b.</span><span class="sxs-lookup"><span data-stu-id="bd44f-198">b.</span></span> <span data-ttu-id="bd44f-199">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd44f-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd44f-200">c.</span><span class="sxs-lookup"><span data-stu-id="bd44f-200">c.</span></span> <span data-ttu-id="bd44f-201">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bd44f-202">d.</span><span class="sxs-lookup"><span data-stu-id="bd44f-202">d.</span></span> <span data-ttu-id="bd44f-203">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="bd44f-204">Tworzenie użytkownika testowego Bonusly</span><span class="sxs-lookup"><span data-stu-id="bd44f-204">Create a Bonusly test user</span></span>

<span data-ttu-id="bd44f-205">Aby umożliwić użytkownikom zalogować się do Bonusly usługi Azure AD, musi być przygotowana do Bonusly.</span><span class="sxs-lookup"><span data-stu-id="bd44f-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="bd44f-206">W przypadku Bonusly Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="bd44f-206">In the case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="bd44f-207">Możesz użyć innych Bonusly użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Bonusly do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="bd44f-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span></span>
>  

<span data-ttu-id="bd44f-208">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bd44f-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="bd44f-209">W oknie przeglądarki sieci web należy zalogować się do dzierżawy Bonusly.</span><span class="sxs-lookup"><span data-stu-id="bd44f-209">In a web browser window, log in to your Bonusly tenant.</span></span>

2. <span data-ttu-id="bd44f-210">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="bd44f-211">![Ustawienia](./media/active-directory-saas-bonus-tutorial/ic781041.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="bd44f-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="bd44f-212">Kliknij przycisk **użytkowników i dodatki** kartę.</span><span class="sxs-lookup"><span data-stu-id="bd44f-212">Click the **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="bd44f-213">![Użytkownicy i dodatki](./media/active-directory-saas-bonus-tutorial/ic781042.png "użytkowników i dodatki")</span><span class="sxs-lookup"><span data-stu-id="bd44f-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="bd44f-214">Kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="bd44f-215">![Zarządzaj użytkownikami](./media/active-directory-saas-bonus-tutorial/ic781043.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="bd44f-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="bd44f-216">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="bd44f-217">![Dodaj użytkownika](./media/active-directory-saas-bonus-tutorial/ic781044.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="bd44f-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="bd44f-218">Na **Dodaj użytkownika** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bd44f-218">On the **Add User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="bd44f-219">![Dodaj użytkownika](./media/active-directory-saas-bonus-tutorial/ic781045.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="bd44f-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="bd44f-220">a.</span><span class="sxs-lookup"><span data-stu-id="bd44f-220">a.</span></span> <span data-ttu-id="bd44f-221">W **imię** pole tekstowe, wprowadź imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-221">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="bd44f-222">b.</span><span class="sxs-lookup"><span data-stu-id="bd44f-222">b.</span></span> <span data-ttu-id="bd44f-223">W **nazwisko** pole tekstowe, wprowadź nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="bd44f-224">c.</span><span class="sxs-lookup"><span data-stu-id="bd44f-224">c.</span></span> <span data-ttu-id="bd44f-225">W **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="bd44f-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="bd44f-226">d.</span><span class="sxs-lookup"><span data-stu-id="bd44f-226">d.</span></span> <span data-ttu-id="bd44f-227">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="bd44f-228">Właściciel konta usługi Azure AD odbiera wiadomość e-mail zawierającą łącze do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="bd44f-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bd44f-229">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44f-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="bd44f-230">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Bonusly.</span><span class="sxs-lookup"><span data-stu-id="bd44f-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="bd44f-232">**Aby przypisać Simona Britta Bonusly, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bd44f-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="bd44f-233">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bd44f-235">Na liście aplikacji zaznacz **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-235">In the applications list, select **Bonusly**.</span></span>

    ![Bonusly łącza na liście aplikacji](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="bd44f-237">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bd44f-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="bd44f-239">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bd44f-239">Click **Add** button.</span></span> <span data-ttu-id="bd44f-240">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd44f-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="bd44f-242">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bd44f-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bd44f-243">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd44f-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd44f-244">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd44f-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bd44f-245">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bd44f-245">Test single sign-on</span></span>

<span data-ttu-id="bd44f-246">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bd44f-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bd44f-247">Po kliknięciu kafelka Bonusly w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane Bonusly aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd44f-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd44f-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bd44f-248">Additional resources</span></span>

* [<span data-ttu-id="bd44f-249">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd44f-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd44f-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd44f-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

