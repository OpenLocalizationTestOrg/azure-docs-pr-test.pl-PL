---
title: 'Samouczek: Integracji Azure Active Directory z Jobbadmin | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Jobbadmin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c5208b0d-66a3-49ed-9aad-70d21f54aee0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 848a6d6d0f072bc3f697ff57756714fc45e7dcc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobbadmin"></a><span data-ttu-id="92f85-103">Samouczek: Integracji Azure Active Directory z Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="92f85-103">Tutorial: Azure Active Directory integration with Jobbadmin</span></span>

<span data-ttu-id="92f85-104">Z tego samouczka dowiesz się integrowanie Jobbadmin z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92f85-104">In this tutorial, you learn how to integrate Jobbadmin with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92f85-105">Integracja z usługą Azure AD Jobbadmin zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="92f85-105">Integrating Jobbadmin with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92f85-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="92f85-106">You can control in Azure AD who has access to Jobbadmin</span></span>
- <span data-ttu-id="92f85-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Jobbadmin (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92f85-107">You can enable your users to automatically get signed-on to Jobbadmin (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92f85-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="92f85-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92f85-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92f85-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92f85-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="92f85-110">Prerequisites</span></span>

<span data-ttu-id="92f85-111">Aby skonfigurować integrację usługi Azure AD z Jobbadmin, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="92f85-111">To configure Azure AD integration with Jobbadmin, you need the following items:</span></span>

- <span data-ttu-id="92f85-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92f85-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92f85-113">Jobbadmin jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="92f85-113">A Jobbadmin single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92f85-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="92f85-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92f85-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="92f85-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92f85-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="92f85-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92f85-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92f85-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92f85-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="92f85-118">Scenario description</span></span>
<span data-ttu-id="92f85-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="92f85-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92f85-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="92f85-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92f85-121">Dodawanie Jobbadmin z galerii</span><span class="sxs-lookup"><span data-stu-id="92f85-121">Adding Jobbadmin from the gallery</span></span>
2. <span data-ttu-id="92f85-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="92f85-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobbadmin-from-the-gallery"></a><span data-ttu-id="92f85-123">Dodawanie Jobbadmin z galerii</span><span class="sxs-lookup"><span data-stu-id="92f85-123">Adding Jobbadmin from the gallery</span></span>
<span data-ttu-id="92f85-124">Aby skonfigurować integrację usługi Azure AD Jobbadmin, należy dodać Jobbadmin z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="92f85-124">To configure the integration of Jobbadmin into Azure AD, you need to add Jobbadmin from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92f85-125">**Aby dodać Jobbadmin z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92f85-125">**To add Jobbadmin from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92f85-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="92f85-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="92f85-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="92f85-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92f85-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="92f85-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="92f85-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92f85-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="92f85-133">W polu wyszukiwania wpisz **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="92f85-133">In the search box, type **Jobbadmin**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_search.png)

5. <span data-ttu-id="92f85-135">W panelu wyników wybierz **Jobbadmin**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="92f85-135">In the results panel, select **Jobbadmin**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92f85-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="92f85-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92f85-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jobbadmin na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="92f85-138">In this section, you configure and test Azure AD single sign-on with Jobbadmin based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="92f85-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Jobbadmin jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92f85-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobbadmin is to a user in Azure AD.</span></span> <span data-ttu-id="92f85-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Jobbadmin musi się.</span><span class="sxs-lookup"><span data-stu-id="92f85-140">In other words, a link relationship between an Azure AD user and the related user in Jobbadmin needs to be established.</span></span>

<span data-ttu-id="92f85-141">W Jobbadmin, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="92f85-141">In Jobbadmin, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92f85-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jobbadmin, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="92f85-142">To configure and test Azure AD single sign-on with Jobbadmin, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92f85-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="92f85-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92f85-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="92f85-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92f85-145">**[Tworzenie użytkownika testowego Jobbadmin](#creating-a-jobbadmin-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Jobbadmin połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92f85-145">**[Creating a Jobbadmin test user](#creating-a-jobbadmin-test-user)** - to have a counterpart of Britta Simon in Jobbadmin that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92f85-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="92f85-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92f85-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="92f85-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92f85-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="92f85-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92f85-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="92f85-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobbadmin application.</span></span>

<span data-ttu-id="92f85-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Jobbadmin, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92f85-150">**To configure Azure AD single sign-on with Jobbadmin, perform the following steps:**</span></span>

1. <span data-ttu-id="92f85-151">W portalu Azure na **Jobbadmin** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="92f85-151">In the Azure portal, on the **Jobbadmin** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="92f85-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="92f85-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_samlbase.png)

3. <span data-ttu-id="92f85-155">Na **Jobbadmin domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92f85-155">On the **Jobbadmin Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_url.png)

    <span data-ttu-id="92f85-157">a.</span><span class="sxs-lookup"><span data-stu-id="92f85-157">a.</span></span> <span data-ttu-id="92f85-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="92f85-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    <span data-ttu-id="92f85-159">b.</span><span class="sxs-lookup"><span data-stu-id="92f85-159">b.</span></span> <span data-ttu-id="92f85-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instancename>.jobnorge.no`</span><span class="sxs-lookup"><span data-stu-id="92f85-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.jobnorge.no`</span></span>

    <span data-ttu-id="92f85-161">c.</span><span class="sxs-lookup"><span data-stu-id="92f85-161">c.</span></span> <span data-ttu-id="92f85-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="92f85-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92f85-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="92f85-163">These values are not real.</span></span> <span data-ttu-id="92f85-164">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="92f85-164">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="92f85-165">Skontaktuj się z [zespołem pomocy technicznej klienta Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="92f85-165">Contact [Jobbadmin Client support team](https://www.jobbnorge.no/om-oss/kontakt-oss) to get these values.</span></span> 
 


4. <span data-ttu-id="92f85-166">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="92f85-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_certificate.png) 

5. <span data-ttu-id="92f85-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="92f85-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92f85-170">Skonfigurować logowanie jednokrotne w **Jobbadmin** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss).</span><span class="sxs-lookup"><span data-stu-id="92f85-170">To configure single sign-on on **Jobbadmin** side, you need to send the downloaded **Metadata XML** to [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss).</span></span> <span data-ttu-id="92f85-171">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="92f85-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="92f85-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="92f85-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92f85-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="92f85-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92f85-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92f85-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92f85-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92f85-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="92f85-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="92f85-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="92f85-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92f85-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92f85-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="92f85-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92f85-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="92f85-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92f85-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92f85-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92f85-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92f85-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92f85-187">a.</span><span class="sxs-lookup"><span data-stu-id="92f85-187">a.</span></span> <span data-ttu-id="92f85-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92f85-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92f85-189">b.</span><span class="sxs-lookup"><span data-stu-id="92f85-189">b.</span></span> <span data-ttu-id="92f85-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92f85-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92f85-191">c.</span><span class="sxs-lookup"><span data-stu-id="92f85-191">c.</span></span> <span data-ttu-id="92f85-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="92f85-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92f85-193">d.</span><span class="sxs-lookup"><span data-stu-id="92f85-193">d.</span></span> <span data-ttu-id="92f85-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="92f85-194">Click **Create**.</span></span>
 
### <a name="creating-a-jobbadmin-test-user"></a><span data-ttu-id="92f85-195">Tworzenie użytkownika testowego Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="92f85-195">Creating a Jobbadmin test user</span></span>

<span data-ttu-id="92f85-196">Aby umożliwić użytkownikom usługi Azure AD zalogować się do Jobbadmin, musi być przygotowana do Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="92f85-196">To enable Azure AD users to log in to Jobbadmin, they must be provisioned into Jobbadmin.</span></span>
 
<span data-ttu-id="92f85-197">Skontaktuj się z [zespołem pomocy technicznej Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss) można pobrać użytkowników dodane w bok.</span><span class="sxs-lookup"><span data-stu-id="92f85-197">Please contact [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss) to get the users added on their side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92f85-198">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92f85-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92f85-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="92f85-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobbadmin.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="92f85-201">**Aby przypisać Simona Britta Jobbadmin, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92f85-201">**To assign Britta Simon to Jobbadmin, perform the following steps:**</span></span>

1. <span data-ttu-id="92f85-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="92f85-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="92f85-204">Na liście aplikacji zaznacz **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="92f85-204">In the applications list, select **Jobbadmin**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_app.png) 

3. <span data-ttu-id="92f85-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="92f85-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="92f85-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="92f85-208">Click **Add** button.</span></span> <span data-ttu-id="92f85-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92f85-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="92f85-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="92f85-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92f85-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92f85-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92f85-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92f85-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92f85-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="92f85-214">Testing single sign-on</span></span>

<span data-ttu-id="92f85-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="92f85-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92f85-216">Po kliknięciu kafelka Jobbadmin w panelu dostępu, należy pobrać strony logowania Jobbadmin aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92f85-216">When you click the Jobbadmin tile in the Access Panel, you should get login page of Jobbadmin application.</span></span>
<span data-ttu-id="92f85-217">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92f85-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="92f85-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="92f85-218">Additional resources</span></span>

* [<span data-ttu-id="92f85-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92f85-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92f85-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92f85-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_203.png

