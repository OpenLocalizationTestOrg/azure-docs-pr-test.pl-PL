---
title: 'Samouczek: Integracji Azure Active Directory z Trakopolis | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Trakopolis."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 3887cf8c085c30eb01ac769944da2fcfe3df81f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="e04ba-103">Samouczek: Integracji Azure Active Directory z Trakopolis</span><span class="sxs-lookup"><span data-stu-id="e04ba-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>

<span data-ttu-id="e04ba-104">Z tego samouczka dowiesz się integrowanie Trakopolis z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e04ba-104">In this tutorial, you learn how to integrate Trakopolis with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e04ba-105">Integracja z usługą Azure AD Trakopolis zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e04ba-105">Integrating Trakopolis with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e04ba-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Trakopolis</span><span class="sxs-lookup"><span data-stu-id="e04ba-106">You can control in Azure AD who has access to Trakopolis</span></span>
- <span data-ttu-id="e04ba-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Trakopolis (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04ba-107">You can enable your users to automatically get signed-on to Trakopolis (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e04ba-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e04ba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e04ba-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e04ba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e04ba-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e04ba-110">Prerequisites</span></span>

<span data-ttu-id="e04ba-111">Aby skonfigurować integrację usługi Azure AD z Trakopolis, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e04ba-111">To configure Azure AD integration with Trakopolis, you need the following items:</span></span>

- <span data-ttu-id="e04ba-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e04ba-113">Trakopolis logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e04ba-113">A Trakopolis single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e04ba-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e04ba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e04ba-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e04ba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e04ba-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e04ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e04ba-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e04ba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e04ba-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e04ba-118">Scenario description</span></span>
<span data-ttu-id="e04ba-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e04ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e04ba-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e04ba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e04ba-121">Dodawanie Trakopolis z galerii</span><span class="sxs-lookup"><span data-stu-id="e04ba-121">Adding Trakopolis from the gallery</span></span>
2. <span data-ttu-id="e04ba-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e04ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-the-gallery"></a><span data-ttu-id="e04ba-123">Dodawanie Trakopolis z galerii</span><span class="sxs-lookup"><span data-stu-id="e04ba-123">Adding Trakopolis from the gallery</span></span>
<span data-ttu-id="e04ba-124">Aby skonfigurować integrację usługi Azure AD Trakopolis, należy dodać Trakopolis z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e04ba-124">To configure the integration of Trakopolis into Azure AD, you need to add Trakopolis from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e04ba-125">**Aby dodać Trakopolis z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e04ba-125">**To add Trakopolis from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e04ba-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e04ba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e04ba-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e04ba-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e04ba-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e04ba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e04ba-133">W polu wyszukiwania wpisz **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-133">In the search box, type **Trakopolis**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_search.png)

5. <span data-ttu-id="e04ba-135">W panelu wyników wybierz **Trakopolis**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e04ba-135">In the results panel, select **Trakopolis**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e04ba-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e04ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e04ba-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Trakopolis w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e04ba-138">In this section, you configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e04ba-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Trakopolis jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e04ba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakopolis is to a user in Azure AD.</span></span> <span data-ttu-id="e04ba-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Trakopolis musi się.</span><span class="sxs-lookup"><span data-stu-id="e04ba-140">In other words, a link relationship between an Azure AD user and the related user in Trakopolis needs to be established.</span></span>

<span data-ttu-id="e04ba-141">W Trakopolis, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="e04ba-141">In Trakopolis, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e04ba-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Trakopolis, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e04ba-142">To configure and test Azure AD single sign-on with Trakopolis, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e04ba-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e04ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e04ba-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e04ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e04ba-145">**[Tworzenie użytkownika testowego Trakopolis](#creating-a-trakopolis-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Trakopolis połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e04ba-145">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - to have a counterpart of Britta Simon in Trakopolis that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e04ba-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e04ba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e04ba-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e04ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e04ba-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e04ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e04ba-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="e04ba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="e04ba-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Trakopolis, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e04ba-150">**To configure Azure AD single sign-on with Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="e04ba-151">W portalu Azure na **Trakopolis** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-151">In the Azure portal, on the **Trakopolis** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e04ba-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e04ba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_samlbase.png)

3. <span data-ttu-id="e04ba-155">Na **Trakopolis domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e04ba-155">On the **Trakopolis Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_url.png)

    <span data-ttu-id="e04ba-157">a.</span><span class="sxs-lookup"><span data-stu-id="e04ba-157">a.</span></span> <span data-ttu-id="e04ba-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.trakopolis.com/`</span><span class="sxs-lookup"><span data-stu-id="e04ba-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com/`</span></span>

    <span data-ttu-id="e04ba-159">b.</span><span class="sxs-lookup"><span data-stu-id="e04ba-159">b.</span></span> <span data-ttu-id="e04ba-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.trakopolis.com`</span><span class="sxs-lookup"><span data-stu-id="e04ba-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e04ba-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e04ba-161">These values are not real.</span></span> <span data-ttu-id="e04ba-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e04ba-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e04ba-163">Skontaktuj się z [zespołem pomocy technicznej klienta Trakopolis](mailto:support@cantelematics.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e04ba-163">Contact [Trakopolis Client support team](mailto:support@cantelematics.com) to get these values.</span></span> 

4. <span data-ttu-id="e04ba-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e04ba-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_certificate.png) 

5. <span data-ttu-id="e04ba-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e04ba-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trakopolis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e04ba-168">Na **konfiguracji Trakopolis** , kliknij przycisk **skonfigurować Trakopolis** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e04ba-168">On the **Trakopolis Configuration** section, click **Configure Trakopolis** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e04ba-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e04ba-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_configure.png) 

7. <span data-ttu-id="e04ba-171">Aby skonfigurować logowanie jednokrotne w **Trakopolis** stronie, musisz wysłać pobrany **XML metadanych, adres URL Sign-Out identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [Trakopolis obsługuje zespół](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="e04ba-171">To configure single sign-on on **Trakopolis** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakopolis support team](mailto:support@cantelematics.com).</span></span> <span data-ttu-id="e04ba-172">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="e04ba-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e04ba-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="e04ba-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e04ba-174">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="e04ba-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e04ba-175">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e04ba-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e04ba-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04ba-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="e04ba-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e04ba-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e04ba-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e04ba-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e04ba-180">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e04ba-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e04ba-182">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e04ba-184">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e04ba-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e04ba-186">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e04ba-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e04ba-188">a.</span><span class="sxs-lookup"><span data-stu-id="e04ba-188">a.</span></span> <span data-ttu-id="e04ba-189">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e04ba-190">b.</span><span class="sxs-lookup"><span data-stu-id="e04ba-190">b.</span></span> <span data-ttu-id="e04ba-191">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e04ba-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e04ba-192">c.</span><span class="sxs-lookup"><span data-stu-id="e04ba-192">c.</span></span> <span data-ttu-id="e04ba-193">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e04ba-194">d.</span><span class="sxs-lookup"><span data-stu-id="e04ba-194">d.</span></span> <span data-ttu-id="e04ba-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-195">Click **Create**.</span></span>
 
### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="e04ba-196">Tworzenie użytkownika testowego Trakopolis</span><span class="sxs-lookup"><span data-stu-id="e04ba-196">Creating a Trakopolis test user</span></span>

<span data-ttu-id="e04ba-197">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="e04ba-197">In this section, you create a user called Britta Simon in Trakopolis.</span></span> <span data-ttu-id="e04ba-198">Praca z [Trakopolis obsługuje zespołu](mailto:support@cantelematics.com) Aby dodać użytkowników do platformy Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="e04ba-198">Work with [Trakopolis support team](mailto:support@cantelematics.com) to add the users in the Trakopolis platform.</span></span> <span data-ttu-id="e04ba-199">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e04ba-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e04ba-200">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04ba-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e04ba-201">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="e04ba-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakopolis.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e04ba-203">**Aby przypisać Simona Britta Trakopolis, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e04ba-203">**To assign Britta Simon to Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="e04ba-204">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e04ba-206">Na liście aplikacji zaznacz **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-206">In the applications list, select **Trakopolis**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_app.png) 

3. <span data-ttu-id="e04ba-208">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e04ba-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e04ba-210">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e04ba-210">Click **Add** button.</span></span> <span data-ttu-id="e04ba-211">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e04ba-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e04ba-213">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e04ba-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e04ba-214">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e04ba-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e04ba-215">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e04ba-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e04ba-216">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e04ba-216">Testing single sign-on</span></span>

<span data-ttu-id="e04ba-217">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e04ba-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="e04ba-218">Po kliknięciu kafelka Trakopolis w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="e04ba-218">When you click the Trakopolis tile in the Access Panel, you should get automatically signed-on to your Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e04ba-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e04ba-219">Additional resources</span></span>

* [<span data-ttu-id="e04ba-220">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e04ba-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e04ba-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e04ba-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png

