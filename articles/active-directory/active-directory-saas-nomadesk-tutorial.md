---
title: 'Samouczek: Integracji Azure Active Directory z Nomadesk | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Nomadesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d261b776-b48e-45f0-9722-0297adefabb8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 1d652d562f4c5caffded18d928e2395e537f59f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadesk"></a><span data-ttu-id="12c9f-103">Samouczek: Integracji Azure Active Directory z Nomadesk</span><span class="sxs-lookup"><span data-stu-id="12c9f-103">Tutorial: Azure Active Directory integration with Nomadesk</span></span>

<span data-ttu-id="12c9f-104">Z tego samouczka dowiesz się integrowanie Nomadesk z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12c9f-104">In this tutorial, you learn how to integrate Nomadesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12c9f-105">Integracja z usługą Azure AD Nomadesk zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="12c9f-105">Integrating Nomadesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="12c9f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Nomadesk</span><span class="sxs-lookup"><span data-stu-id="12c9f-106">You can control in Azure AD who has access to Nomadesk</span></span>
- <span data-ttu-id="12c9f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Nomadesk (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c9f-107">You can enable your users to automatically get signed-on to Nomadesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="12c9f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="12c9f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="12c9f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="12c9f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12c9f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="12c9f-110">Prerequisites</span></span>

<span data-ttu-id="12c9f-111">Aby skonfigurować integrację usługi Azure AD z Nomadesk, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="12c9f-111">To configure Azure AD integration with Nomadesk, you need the following items:</span></span>

- <span data-ttu-id="12c9f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c9f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12c9f-113">Nomadesk logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="12c9f-113">A Nomadesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12c9f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="12c9f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12c9f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="12c9f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12c9f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="12c9f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12c9f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12c9f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12c9f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="12c9f-118">Scenario description</span></span>
<span data-ttu-id="12c9f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="12c9f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12c9f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="12c9f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12c9f-121">Dodawanie Nomadesk z galerii</span><span class="sxs-lookup"><span data-stu-id="12c9f-121">Adding Nomadesk from the gallery</span></span>
2. <span data-ttu-id="12c9f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="12c9f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nomadesk-from-the-gallery"></a><span data-ttu-id="12c9f-123">Dodawanie Nomadesk z galerii</span><span class="sxs-lookup"><span data-stu-id="12c9f-123">Adding Nomadesk from the gallery</span></span>
<span data-ttu-id="12c9f-124">Aby skonfigurować integrację usługi Azure AD Nomadesk, należy dodać Nomadesk z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="12c9f-124">To configure the integration of Nomadesk into Azure AD, you need to add Nomadesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="12c9f-125">**Aby dodać Nomadesk z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="12c9f-125">**To add Nomadesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="12c9f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="12c9f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="12c9f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="12c9f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="12c9f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="12c9f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="12c9f-133">W polu wyszukiwania wpisz **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-133">In the search box, type **Nomadesk**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_search.png)

5. <span data-ttu-id="12c9f-135">W panelu wyników wybierz **Nomadesk**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="12c9f-135">In the results panel, select **Nomadesk**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="12c9f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="12c9f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="12c9f-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Nomadesk w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="12c9f-138">In this section, you configure and test Azure AD single sign-on with Nomadesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="12c9f-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Nomadesk jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12c9f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadesk is to a user in Azure AD.</span></span> <span data-ttu-id="12c9f-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Nomadesk musi się.</span><span class="sxs-lookup"><span data-stu-id="12c9f-140">In other words, a link relationship between an Azure AD user and the related user in Nomadesk needs to be established.</span></span>

<span data-ttu-id="12c9f-141">W Nomadesk, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="12c9f-141">In Nomadesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="12c9f-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Nomadesk, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="12c9f-142">To configure and test Azure AD single sign-on with Nomadesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="12c9f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="12c9f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="12c9f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="12c9f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12c9f-145">**[Tworzenie użytkownika testowego Nomadesk](#creating-a-nomadesk-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Nomadesk połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="12c9f-145">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - to have a counterpart of Britta Simon in Nomadesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="12c9f-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="12c9f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12c9f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="12c9f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="12c9f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="12c9f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="12c9f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="12c9f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadesk application.</span></span>

<span data-ttu-id="12c9f-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Nomadesk, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="12c9f-150">**To configure Azure AD single sign-on with Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="12c9f-151">W portalu Azure na **Nomadesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-151">In the Azure portal, on the **Nomadesk** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="12c9f-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="12c9f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_samlbase.png)

3. <span data-ttu-id="12c9f-155">Na **Nomadesk domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="12c9f-155">On the **Nomadesk Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_url.png)

    <span data-ttu-id="12c9f-157">a.</span><span class="sxs-lookup"><span data-stu-id="12c9f-157">a.</span></span> <span data-ttu-id="12c9f-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://mynomadesk.com/logon/saml/<TENANTID>`</span><span class="sxs-lookup"><span data-stu-id="12c9f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mynomadesk.com/logon/saml/<TENANTID>`</span></span>

    <span data-ttu-id="12c9f-159">b.</span><span class="sxs-lookup"><span data-stu-id="12c9f-159">b.</span></span> <span data-ttu-id="12c9f-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://secure.nomadesk.com/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="12c9f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://secure.nomadesk.com/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="12c9f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="12c9f-161">These values are not real.</span></span> <span data-ttu-id="12c9f-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="12c9f-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="12c9f-163">Skontaktuj się z [zespołem pomocy technicznej klienta Nomadesk](mailto:support@nomadesk.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="12c9f-163">Contact [Nomadesk Client support team](mailto:support@nomadesk.com) to get these values.</span></span> 
 
4. <span data-ttu-id="12c9f-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="12c9f-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_certificate.png) 

5. <span data-ttu-id="12c9f-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="12c9f-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nomadesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="12c9f-168">Na **konfiguracji Nomadesk** , kliknij przycisk **skonfigurować Nomadesk** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="12c9f-168">On the **Nomadesk Configuration** section, click **Configure Nomadesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="12c9f-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="12c9f-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_configure.png) 

7. <span data-ttu-id="12c9f-171">Do konfigurowania rejestracji jednokrotnej na **Nomadesk** stronie, musisz wysłać pobrany **certyfikatu**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [Zespołem pomocy technicznej Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="12c9f-171">To configure single sign-on on **Nomadesk** side, you need to send the downloaded **Certificate**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Nomadesk support team](mailto:support@nomadesk.com).</span></span> <span data-ttu-id="12c9f-172">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="12c9f-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="12c9f-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="12c9f-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="12c9f-174">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="12c9f-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="12c9f-175">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="12c9f-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="12c9f-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c9f-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="12c9f-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="12c9f-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="12c9f-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="12c9f-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="12c9f-180">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="12c9f-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="12c9f-182">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="12c9f-184">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="12c9f-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="12c9f-186">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="12c9f-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="12c9f-188">a.</span><span class="sxs-lookup"><span data-stu-id="12c9f-188">a.</span></span> <span data-ttu-id="12c9f-189">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12c9f-190">b.</span><span class="sxs-lookup"><span data-stu-id="12c9f-190">b.</span></span> <span data-ttu-id="12c9f-191">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="12c9f-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="12c9f-192">c.</span><span class="sxs-lookup"><span data-stu-id="12c9f-192">c.</span></span> <span data-ttu-id="12c9f-193">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="12c9f-194">d.</span><span class="sxs-lookup"><span data-stu-id="12c9f-194">d.</span></span> <span data-ttu-id="12c9f-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-195">Click **Create**.</span></span>
 
### <a name="creating-a-nomadesk-test-user"></a><span data-ttu-id="12c9f-196">Tworzenie użytkownika testowego Nomadesk</span><span class="sxs-lookup"><span data-stu-id="12c9f-196">Creating a Nomadesk test user</span></span>

<span data-ttu-id="12c9f-197">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="12c9f-197">The objective of this section is to create a user called Britta Simon in Nomadesk.</span></span> <span data-ttu-id="12c9f-198">Nomadesk obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="12c9f-198">Nomadesk supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="12c9f-199">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="12c9f-199">There is no action item for you in this section.</span></span> <span data-ttu-id="12c9f-200">Nowy użytkownik został utworzony podczas próby dostępu Nomadesk, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="12c9f-200">A new user is created during an attempt to access Nomadesk if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="12c9f-201">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="12c9f-201">If you need to create a user manually, you need to contact the [Nomadesk support team](mailto:support@nomadesk.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="12c9f-202">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c9f-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="12c9f-203">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="12c9f-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadesk.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="12c9f-205">**Aby przypisać Simona Britta Nomadesk, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="12c9f-205">**To assign Britta Simon to Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="12c9f-206">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="12c9f-208">Na liście aplikacji zaznacz **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-208">In the applications list, select **Nomadesk**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_app.png) 

3. <span data-ttu-id="12c9f-210">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="12c9f-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="12c9f-212">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="12c9f-212">Click **Add** button.</span></span> <span data-ttu-id="12c9f-213">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="12c9f-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="12c9f-215">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="12c9f-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="12c9f-216">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="12c9f-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12c9f-217">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="12c9f-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="12c9f-218">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="12c9f-218">Testing single sign-on</span></span>

<span data-ttu-id="12c9f-219">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="12c9f-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="12c9f-220">Po kliknięciu kafelka Nomadesk w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="12c9f-220">When you click the Nomadesk tile in the Access Panel,  you should get automatically signed-on to your Nomadesk application.</span></span>
<span data-ttu-id="12c9f-221">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="12c9f-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12c9f-222">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="12c9f-222">Additional resources</span></span>

* [<span data-ttu-id="12c9f-223">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12c9f-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12c9f-224">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="12c9f-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_203.png

