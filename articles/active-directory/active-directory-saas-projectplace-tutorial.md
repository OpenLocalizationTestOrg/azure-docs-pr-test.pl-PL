---
title: 'Samouczek: Integracji Azure Active Directory z Projectplace | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Projectplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: bb9dd10c887cb0e42e544066d9b0dcfa554e10ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="98279-103">Samouczek: Integracji Azure Active Directory z Projectplace</span><span class="sxs-lookup"><span data-stu-id="98279-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="98279-104">Z tego samouczka dowiesz się integrowanie Projectplace z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98279-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98279-105">Integracja z usługą Azure AD Projectplace zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="98279-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="98279-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Projectplace</span><span class="sxs-lookup"><span data-stu-id="98279-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="98279-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Projectplace (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="98279-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="98279-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="98279-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="98279-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="98279-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98279-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="98279-110">Prerequisites</span></span>

<span data-ttu-id="98279-111">Aby skonfigurować integrację usługi Azure AD z Projectplace, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="98279-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="98279-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="98279-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98279-113">Projectplace logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="98279-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98279-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="98279-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="98279-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="98279-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98279-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="98279-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98279-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98279-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98279-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="98279-118">Scenario description</span></span>
<span data-ttu-id="98279-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="98279-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98279-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="98279-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98279-121">Dodawanie Projectplace z galerii</span><span class="sxs-lookup"><span data-stu-id="98279-121">Adding Projectplace from the gallery</span></span>
2. <span data-ttu-id="98279-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="98279-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="98279-123">Dodawanie Projectplace z galerii</span><span class="sxs-lookup"><span data-stu-id="98279-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="98279-124">Aby skonfigurować integrację usługi Azure AD Projectplace, należy dodać Projectplace z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="98279-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="98279-125">**Aby dodać Projectplace z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="98279-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="98279-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="98279-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="98279-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="98279-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="98279-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="98279-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="98279-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="98279-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="98279-133">W polu wyszukiwania wpisz **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="98279-133">In the search box, type **Projectplace**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="98279-135">W panelu wyników wybierz **Projectplace**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="98279-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="98279-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="98279-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="98279-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Projectplace w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="98279-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="98279-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Projectplace jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98279-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="98279-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Projectplace musi się.</span><span class="sxs-lookup"><span data-stu-id="98279-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="98279-141">W Projectplace, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="98279-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="98279-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Projectplace, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="98279-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="98279-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="98279-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="98279-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="98279-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="98279-145">**[Tworzenie użytkownika testowego Projectplace](#creating-a-projectplace-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Projectplace połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="98279-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="98279-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="98279-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="98279-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="98279-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="98279-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="98279-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="98279-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Projectplace.</span><span class="sxs-lookup"><span data-stu-id="98279-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="98279-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Projectplace, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="98279-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="98279-151">W portalu Azure na **Projectplace** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="98279-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="98279-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="98279-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="98279-155">Na **Projectplace domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="98279-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="98279-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="98279-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="98279-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="98279-158">This value is not real.</span></span> <span data-ttu-id="98279-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="98279-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="98279-160">Skontaktuj się z [zespołem pomocy technicznej klienta Projectplace](https://success.planview.com/Projectplace/Support) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="98279-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
4. <span data-ttu-id="98279-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="98279-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="98279-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="98279-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="98279-165">Skonfigurować logowanie jednokrotne w **Projectplace** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="98279-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="98279-166">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="98279-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="98279-167">Pojedynczą konfiguracją logowania jednokrotnego musi zostać wykonana przez [zespołem pomocy technicznej Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="98279-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="98279-168">Otrzymasz powiadomienie, natychmiast po zakończeniu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="98279-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="98279-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="98279-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="98279-170">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="98279-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="98279-171">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="98279-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="98279-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="98279-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="98279-173">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="98279-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="98279-175">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="98279-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="98279-176">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="98279-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="98279-178">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="98279-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="98279-180">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="98279-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="98279-182">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="98279-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="98279-184">a.</span><span class="sxs-lookup"><span data-stu-id="98279-184">a.</span></span> <span data-ttu-id="98279-185">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="98279-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98279-186">b.</span><span class="sxs-lookup"><span data-stu-id="98279-186">b.</span></span> <span data-ttu-id="98279-187">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="98279-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="98279-188">c.</span><span class="sxs-lookup"><span data-stu-id="98279-188">c.</span></span> <span data-ttu-id="98279-189">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="98279-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="98279-190">d.</span><span class="sxs-lookup"><span data-stu-id="98279-190">d.</span></span> <span data-ttu-id="98279-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="98279-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="98279-192">Tworzenie użytkownika testowego Projectplace</span><span class="sxs-lookup"><span data-stu-id="98279-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="98279-193">Aby włączyć użytkowników usługi Azure AD zalogować się do Projectplace, musi być przygotowana do Projectplace.</span><span class="sxs-lookup"><span data-stu-id="98279-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="98279-194">W przypadku Projectplace Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="98279-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="98279-195">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="98279-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="98279-196">Zaloguj się do Twojego **Projectplace** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="98279-196">Log in to your **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="98279-197">Przejdź do **osób**, a następnie kliknij przycisk **członków**.</span><span class="sxs-lookup"><span data-stu-id="98279-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="98279-198">![Osoby](./media/active-directory-saas-projectplace-tutorial/ic790228.png "osób")</span><span class="sxs-lookup"><span data-stu-id="98279-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="98279-199">Kliknij przycisk **dodać członka**.</span><span class="sxs-lookup"><span data-stu-id="98279-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="98279-200">![Dodawanie członków](./media/active-directory-saas-projectplace-tutorial/ic790232.png "dodawać członków")</span><span class="sxs-lookup"><span data-stu-id="98279-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="98279-201">W **dodać element członkowski** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="98279-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="98279-202">![Nowe elementy członkowskie](./media/active-directory-saas-projectplace-tutorial/ic790233.png "nowych elementów członkowskich")</span><span class="sxs-lookup"><span data-stu-id="98279-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="98279-203">a.</span><span class="sxs-lookup"><span data-stu-id="98279-203">a.</span></span> <span data-ttu-id="98279-204">W **nowe elementy członkowskie** tekstowym, wpisz adres e-mail prawidłowego konta usługi AAD ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="98279-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="98279-205">b.</span><span class="sxs-lookup"><span data-stu-id="98279-205">b.</span></span> <span data-ttu-id="98279-206">Kliknij przycisk **wysyłania**.</span><span class="sxs-lookup"><span data-stu-id="98279-206">Click **Send**.</span></span>

   <span data-ttu-id="98279-207">Do właściciela konta usługi Azure Active Directory zostanie wysłana wiadomość e-mail, łącznie z łączem do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="98279-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="98279-208">Możesz użyć innych Projectplace użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Projectplace do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="98279-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="98279-209">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="98279-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="98279-210">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Projectplace.</span><span class="sxs-lookup"><span data-stu-id="98279-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="98279-212">**Aby przypisać Simona Britta Projectplace, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="98279-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="98279-213">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="98279-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="98279-215">Na liście aplikacji zaznacz **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="98279-215">In the applications list, select **Projectplace**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="98279-217">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="98279-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="98279-219">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="98279-219">Click **Add** button.</span></span> <span data-ttu-id="98279-220">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="98279-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="98279-222">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="98279-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="98279-223">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="98279-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="98279-224">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="98279-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="98279-225">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="98279-225">Testing single sign-on</span></span>

<span data-ttu-id="98279-226">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="98279-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="98279-227">Po kliknięciu kafelka Projectplace w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Projectplace.</span><span class="sxs-lookup"><span data-stu-id="98279-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="98279-228">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="98279-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98279-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="98279-229">Additional resources</span></span>

* [<span data-ttu-id="98279-230">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98279-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="98279-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="98279-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

