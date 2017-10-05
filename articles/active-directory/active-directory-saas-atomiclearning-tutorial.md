---
title: 'Samouczek: Integracji Azure Active Directory z Atomic Learning | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługi Azure Active Directory i uczenie się Atomic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 6cce8fc839e60eb6498ab48bf68e9906c98889a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="57546-103">Samouczek: Integracji Azure Active Directory z Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="57546-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="57546-104">Z tego samouczka dowiesz się integrowanie Atomic Learning z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57546-104">In this tutorial, you learn how to integrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57546-105">Integrowanie Atomic Learning z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="57546-105">Integrating Atomic Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57546-106">Można kontrolować w usłudze Azure AD, który ma dostęp do uczenia Atomic</span><span class="sxs-lookup"><span data-stu-id="57546-106">You can control in Azure AD who has access to Atomic Learning</span></span>
- <span data-ttu-id="57546-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do uczenia niepodzielne (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="57546-107">You can enable your users to automatically get signed-on to Atomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57546-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="57546-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="57546-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57546-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57546-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="57546-110">Prerequisites</span></span>

<span data-ttu-id="57546-111">Aby skonfigurować integrację usługi Azure AD przy użyciu Atomic Learning, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="57546-111">To configure Azure AD integration with Atomic Learning, you need the following items:</span></span>

- <span data-ttu-id="57546-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="57546-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57546-113">Atomic Learning jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="57546-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57546-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="57546-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57546-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="57546-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57546-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="57546-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57546-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57546-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57546-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="57546-118">Scenario description</span></span>
<span data-ttu-id="57546-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="57546-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57546-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="57546-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57546-121">Dodawanie Atomic uczenia z galerii</span><span class="sxs-lookup"><span data-stu-id="57546-121">Adding Atomic Learning from the gallery</span></span>
2. <span data-ttu-id="57546-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="57546-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-the-gallery"></a><span data-ttu-id="57546-123">Dodawanie Atomic uczenia z galerii</span><span class="sxs-lookup"><span data-stu-id="57546-123">Adding Atomic Learning from the gallery</span></span>
<span data-ttu-id="57546-124">Aby skonfigurować integrację Atomic Learning z usługą Azure AD, należy dodać Atomic uczenia z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="57546-124">To configure the integration of Atomic Learning into Azure AD, you need to add Atomic Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57546-125">**Aby dodać Atomic uczenia z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="57546-125">**To add Atomic Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57546-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="57546-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="57546-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="57546-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57546-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="57546-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="57546-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57546-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="57546-133">W polu wyszukiwania wpisz **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="57546-133">In the search box, type **Atomic Learning**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="57546-135">W panelu wyników wybierz **Atomic Learning**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="57546-135">In the results panel, select **Atomic Learning**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57546-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="57546-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57546-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD logowania jednokrotnego przy użyciu Atomic Learning na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="57546-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="57546-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w uczeniu Atomic jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57546-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atomic Learning is to a user in Azure AD.</span></span> <span data-ttu-id="57546-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w uczeniu Atomic musi się.</span><span class="sxs-lookup"><span data-stu-id="57546-140">In other words, a link relationship between an Azure AD user and the related user in Atomic Learning needs to be established.</span></span>

<span data-ttu-id="57546-141">W uczeniu Atomic przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="57546-141">In Atomic Learning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="57546-142">Do konfigurowania i testowania usługi Azure AD logowania jednokrotnego przy użyciu Atomic Learning, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="57546-142">To configure and test Azure AD single sign-on with Atomic Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57546-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="57546-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57546-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="57546-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57546-145">**[Tworzenie użytkownika testowego Atomic Learning](#creating-an-atomic-learning-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Atomic zapoznanie się z jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="57546-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - to have a counterpart of Britta Simon in Atomic Learning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="57546-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="57546-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57546-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="57546-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57546-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="57546-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57546-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="57546-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="57546-150">**Aby skonfigurować usługi Azure AD logowania jednokrotnego przy użyciu Atomic Learning, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="57546-150">**To configure Azure AD single sign-on with Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="57546-151">W portalu Azure na **Atomic Learning** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="57546-151">In the Azure portal, on the **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="57546-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="57546-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="57546-155">Na **Atomic domeny uczenie i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="57546-155">On the **Atomic Learning Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="57546-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="57546-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="57546-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="57546-158">This value is not real.</span></span> <span data-ttu-id="57546-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="57546-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="57546-160">Skontaktuj się z [zespołem pomocy technicznej klienta Learning Atomic](mailto:cs@atomiclearning.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="57546-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) to get this value.</span></span> 
 
4. <span data-ttu-id="57546-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="57546-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="57546-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="57546-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57546-165">Skonfigurować logowanie jednokrotne w **Atomic Learning** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Atomic Learning](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="57546-165">To configure single sign-on on **Atomic Learning** side, you need to send the downloaded **Metadata XML** to [Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="57546-166">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="57546-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="57546-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="57546-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="57546-168">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="57546-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="57546-169">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57546-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57546-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="57546-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="57546-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="57546-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="57546-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="57546-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57546-174">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="57546-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57546-176">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="57546-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57546-178">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57546-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57546-180">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="57546-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57546-182">a.</span><span class="sxs-lookup"><span data-stu-id="57546-182">a.</span></span> <span data-ttu-id="57546-183">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57546-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57546-184">b.</span><span class="sxs-lookup"><span data-stu-id="57546-184">b.</span></span> <span data-ttu-id="57546-185">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57546-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57546-186">c.</span><span class="sxs-lookup"><span data-stu-id="57546-186">c.</span></span> <span data-ttu-id="57546-187">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="57546-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57546-188">d.</span><span class="sxs-lookup"><span data-stu-id="57546-188">d.</span></span> <span data-ttu-id="57546-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="57546-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="57546-190">Tworzenie użytkownika testowego Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="57546-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="57546-191">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w uczeniu Atomic.</span><span class="sxs-lookup"><span data-stu-id="57546-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="57546-192">Atomic Learning obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="57546-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="57546-193">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="57546-193">There is no action item for you in this section.</span></span> <span data-ttu-id="57546-194">Nowy użytkownik został utworzony podczas próby dostępu Atomic uczenia, jeśli nie istnieje jeszcze przy użyciu adresu e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="57546-194">A new user is created during an attempt to access Atomic Learning if it doesn't exist yet using the email address for the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="57546-195">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="57546-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="57546-196">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do uczenia Atomic.</span><span class="sxs-lookup"><span data-stu-id="57546-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atomic Learning.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="57546-198">**Aby przypisać Simona Britta Atomic uczenia, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="57546-198">**To assign Britta Simon to Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="57546-199">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="57546-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="57546-201">Na liście aplikacji zaznacz **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="57546-201">In the applications list, select **Atomic Learning**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="57546-203">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="57546-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="57546-205">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="57546-205">Click **Add** button.</span></span> <span data-ttu-id="57546-206">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57546-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="57546-208">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="57546-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57546-209">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57546-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57546-210">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57546-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57546-211">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="57546-211">Testing single sign-on</span></span>

<span data-ttu-id="57546-212">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="57546-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="57546-213">Po kliknięciu kafelka Atomic Learning w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="57546-213">When you click the Atomic Learning tile in the Access Panel, you should get automatically signed-on to your Atomic Learning application.</span></span>
<span data-ttu-id="57546-214">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="57546-214">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="57546-215">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="57546-215">Additional resources</span></span>

* [<span data-ttu-id="57546-216">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57546-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57546-217">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57546-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png

