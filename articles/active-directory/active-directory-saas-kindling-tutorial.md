---
title: 'Samouczek: Integracji Azure Active Directory z Kindling | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Kindling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 131c2c3f46c60193d512b1779e917c8322732fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="77f83-103">Samouczek: Integracji Azure Active Directory z Kindling</span><span class="sxs-lookup"><span data-stu-id="77f83-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="77f83-104">Z tego samouczka dowiesz się integrowanie Kindling z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77f83-104">In this tutorial, you learn how to integrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77f83-105">Integracja z usługą Azure AD Kindling zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="77f83-105">Integrating Kindling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="77f83-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Kindling</span><span class="sxs-lookup"><span data-stu-id="77f83-106">You can control in Azure AD who has access to Kindling</span></span>
- <span data-ttu-id="77f83-107">Można umożliwić użytkownikom automatycznie pobrać zalogowane do Kindling (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="77f83-107">You can enable your users to automatically get signed-on to Kindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77f83-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="77f83-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="77f83-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="77f83-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="77f83-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77f83-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77f83-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77f83-111">Prerequisites</span></span>

<span data-ttu-id="77f83-112">Aby skonfigurować integrację usługi Azure AD z Kindling, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="77f83-112">To configure Azure AD integration with Kindling, you need the following items:</span></span>

- <span data-ttu-id="77f83-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="77f83-113">An Azure AD subscription</span></span>
- <span data-ttu-id="77f83-114">Kindling logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="77f83-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77f83-115">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="77f83-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77f83-116">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="77f83-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77f83-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="77f83-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77f83-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77f83-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77f83-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="77f83-119">Scenario description</span></span>
<span data-ttu-id="77f83-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="77f83-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77f83-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="77f83-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77f83-122">Dodawanie Kindling z galerii</span><span class="sxs-lookup"><span data-stu-id="77f83-122">Adding Kindling from the gallery</span></span>
2. <span data-ttu-id="77f83-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="77f83-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-the-gallery"></a><span data-ttu-id="77f83-124">Dodawanie Kindling z galerii</span><span class="sxs-lookup"><span data-stu-id="77f83-124">Adding Kindling from the gallery</span></span>
<span data-ttu-id="77f83-125">Aby skonfigurować integrację Kindling do usługi Azure AD, należy dodać Kindling z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="77f83-125">To configure the integration of Kindling into Azure AD, you need to add Kindling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="77f83-126">**Aby dodać Kindling z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="77f83-126">**To add Kindling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="77f83-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="77f83-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="77f83-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="77f83-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="77f83-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="77f83-130">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="77f83-132">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77f83-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="77f83-134">W polu wyszukiwania wpisz **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="77f83-134">In the search box, type **Kindling**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="77f83-136">W panelu wyników wybierz **Kindling**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="77f83-136">In the results panel, select **Kindling**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77f83-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="77f83-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77f83-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kindling na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="77f83-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="77f83-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Kindling jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77f83-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Kindling is to a user in Azure AD.</span></span> <span data-ttu-id="77f83-141">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Kindling powinien być określony.</span><span class="sxs-lookup"><span data-stu-id="77f83-141">In other words, a link relationship between an Azure AD user and the related user in Kindling needs to be established.</span></span>

<span data-ttu-id="77f83-142">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Kindling.</span><span class="sxs-lookup"><span data-stu-id="77f83-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kindling.</span></span>

<span data-ttu-id="77f83-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kindling, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="77f83-143">To configure and test Azure AD single sign-on with Kindling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="77f83-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="77f83-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="77f83-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="77f83-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77f83-146">**[Tworzenie użytkownika testowego Kindling](#creating-a-kindling-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Kindling połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="77f83-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - to have a counterpart of Britta Simon in Kindling that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="77f83-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="77f83-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77f83-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="77f83-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77f83-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="77f83-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77f83-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Kindling.</span><span class="sxs-lookup"><span data-stu-id="77f83-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="77f83-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Kindling, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="77f83-151">**To configure Azure AD single sign-on with Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="77f83-152">W portalu Azure na **Kindling** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="77f83-152">In the Azure portal, on the **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="77f83-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="77f83-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="77f83-156">Na **Kindling domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="77f83-156">On the **Kindling Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="77f83-158">a.</span><span class="sxs-lookup"><span data-stu-id="77f83-158">a.</span></span> <span data-ttu-id="77f83-159">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="77f83-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="77f83-160">b.</span><span class="sxs-lookup"><span data-stu-id="77f83-160">b.</span></span>  <span data-ttu-id="77f83-161">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="77f83-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="77f83-162">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="77f83-162">These values are not the real.</span></span> <span data-ttu-id="77f83-163">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="77f83-163">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="77f83-164">Skontaktuj się z [zespołem pomocy technicznej Kindling](mailto:support@kindlingapp.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="77f83-164">Contact [Kindling support team](mailto:support@kindlingapp.com) to get these values.</span></span>
 
4. <span data-ttu-id="77f83-165">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="77f83-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="77f83-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="77f83-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77f83-169">Na **Kindling konfiguracji** kliknij **skonfigurować Kindling** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="77f83-169">On the **Kindling Configuration** section, click **Configure Kindling** to open **Configure sign-on** window.</span></span> <span data-ttu-id="77f83-170">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="77f83-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="77f83-172">Do konfigurowania rejestracji jednokrotnej na **Kindling** stronie, musisz wysłać pobrany **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi**do [zespołem pomocy technicznej Kindling](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="77f83-172">To configure single sign-on on **Kindling** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="77f83-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="77f83-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="77f83-174">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="77f83-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="77f83-175">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77f83-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77f83-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="77f83-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="77f83-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="77f83-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="77f83-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="77f83-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="77f83-180">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="77f83-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77f83-182">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="77f83-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77f83-184">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77f83-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77f83-186">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="77f83-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77f83-188">a.</span><span class="sxs-lookup"><span data-stu-id="77f83-188">a.</span></span> <span data-ttu-id="77f83-189">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77f83-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77f83-190">b.</span><span class="sxs-lookup"><span data-stu-id="77f83-190">b.</span></span> <span data-ttu-id="77f83-191">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="77f83-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77f83-192">c.</span><span class="sxs-lookup"><span data-stu-id="77f83-192">c.</span></span> <span data-ttu-id="77f83-193">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="77f83-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="77f83-194">d.</span><span class="sxs-lookup"><span data-stu-id="77f83-194">d.</span></span> <span data-ttu-id="77f83-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="77f83-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="77f83-196">Tworzenie użytkownika testowego Kindling</span><span class="sxs-lookup"><span data-stu-id="77f83-196">Creating a Kindling test user</span></span>

<span data-ttu-id="77f83-197">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Kindling.</span><span class="sxs-lookup"><span data-stu-id="77f83-197">The objective of this section is to create a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="77f83-198">Kindling obsługę w czasie.</span><span class="sxs-lookup"><span data-stu-id="77f83-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="77f83-199">Została już włączona w [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="77f83-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="77f83-200">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="77f83-200">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="77f83-201">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="77f83-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="77f83-202">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Kindling.</span><span class="sxs-lookup"><span data-stu-id="77f83-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kindling.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="77f83-204">**Aby przypisać Simona Britta Kindling, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="77f83-204">**To assign Britta Simon to Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="77f83-205">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="77f83-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="77f83-207">Na liście aplikacji zaznacz **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="77f83-207">In the applications list, select **Kindling**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="77f83-209">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="77f83-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="77f83-211">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="77f83-211">Click **Add** button.</span></span> <span data-ttu-id="77f83-212">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77f83-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="77f83-214">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="77f83-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="77f83-215">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77f83-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77f83-216">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77f83-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77f83-217">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="77f83-217">Testing single sign-on</span></span>

<span data-ttu-id="77f83-218">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="77f83-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="77f83-219">Po kliknięciu kafelka Kindling w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Kindling.</span><span class="sxs-lookup"><span data-stu-id="77f83-219">When you click the Kindling tile in the Access Panel, you should get automatically signed-on to your Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="77f83-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="77f83-220">Additional resources</span></span>

* [<span data-ttu-id="77f83-221">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77f83-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77f83-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77f83-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

