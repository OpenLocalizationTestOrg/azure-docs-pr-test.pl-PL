---
title: 'Samouczek: Integracji Azure Active Directory z LMS stanowisko Learning | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i LMS stanowisko Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: 877e0288fdd1f590acf064c204aff0741539b112
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="96f1e-103">Samouczek: Integracji Azure Active Directory z LMS stanowisko Learning</span><span class="sxs-lookup"><span data-stu-id="96f1e-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="96f1e-104">Z tego samouczka dowiesz się integrowanie LMS stanowisko Learning z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96f1e-104">In this tutorial, you learn how to integrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96f1e-105">Integrowanie LMS stanowisko Learning z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="96f1e-105">Integrating Learning Seat LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="96f1e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do LMS stanowisko Learning</span><span class="sxs-lookup"><span data-stu-id="96f1e-106">You can control in Azure AD who has access to Learning Seat LMS</span></span>
- <span data-ttu-id="96f1e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do uczenia stanowisko LMS (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f1e-107">You can enable your users to automatically get signed-on to Learning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96f1e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="96f1e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="96f1e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="96f1e-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="96f1e-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96f1e-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96f1e-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="96f1e-111">Prerequisites</span></span>

<span data-ttu-id="96f1e-112">Aby skonfigurować integrację usługi Azure AD z Learning stanowisko LMS, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="96f1e-112">To configure Azure AD integration with Learning Seat LMS, you need the following items:</span></span>

- <span data-ttu-id="96f1e-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f1e-113">An Azure AD subscription</span></span>
- <span data-ttu-id="96f1e-114">Learning stanowisko LMS jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="96f1e-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96f1e-115">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="96f1e-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96f1e-116">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="96f1e-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96f1e-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="96f1e-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96f1e-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96f1e-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96f1e-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="96f1e-119">Scenario description</span></span>
<span data-ttu-id="96f1e-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="96f1e-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96f1e-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="96f1e-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96f1e-122">Dodawanie LMS stanowisko Learning z galerii</span><span class="sxs-lookup"><span data-stu-id="96f1e-122">Adding Learning Seat LMS from the gallery</span></span>
2. <span data-ttu-id="96f1e-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="96f1e-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-the-gallery"></a><span data-ttu-id="96f1e-124">Dodawanie LMS stanowisko Learning z galerii</span><span class="sxs-lookup"><span data-stu-id="96f1e-124">Adding Learning Seat LMS from the gallery</span></span>
<span data-ttu-id="96f1e-125">Aby skonfigurować integrację LMS stanowisko Learning z usługą Azure AD, należy dodać LMS stanowisko Learning z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="96f1e-125">To configure the integration of Learning Seat LMS into Azure AD, you need to add Learning Seat LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="96f1e-126">**Aby dodać LMS stanowisko Learning z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="96f1e-126">**To add Learning Seat LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="96f1e-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="96f1e-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="96f1e-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="96f1e-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-130">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="96f1e-132">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f1e-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="96f1e-134">W polu wyszukiwania wpisz **LMS stanowisko Learning**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-134">In the search box, type **Learning Seat LMS**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="96f1e-136">W panelu wyników wybierz **LMS stanowisko Learning**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="96f1e-136">In the results panel, select **Learning Seat LMS**, and then click **Add** button to add the application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96f1e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="96f1e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96f1e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LMS stanowisko uczenie na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="96f1e-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="96f1e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w LMS stanowisko Learning jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f1e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning Seat LMS is to a user in Azure AD.</span></span> <span data-ttu-id="96f1e-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w LMS stanowisko Learning musi się.</span><span class="sxs-lookup"><span data-stu-id="96f1e-140">In other words, a link relationship between an Azure AD user and the related user in Learning Seat LMS needs to be established.</span></span>

<span data-ttu-id="96f1e-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w LMS stanowisko Learning.</span><span class="sxs-lookup"><span data-stu-id="96f1e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="96f1e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LMS stanowisko Learning, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="96f1e-142">To configure and test Azure AD single sign-on with Learning Seat LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="96f1e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="96f1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="96f1e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="96f1e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96f1e-145">**[Tworzenie użytkownika testowego LMS stanowisko Learning](#creating-a-learnconnect-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta LMS stanowisko Learning połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="96f1e-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - to have a counterpart of Britta Simon in Learning Seat LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="96f1e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="96f1e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96f1e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="96f1e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96f1e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="96f1e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96f1e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji LMS stanowisko Learning.</span><span class="sxs-lookup"><span data-stu-id="96f1e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="96f1e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z LMS stanowisko Learning, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="96f1e-150">**To configure Azure AD single sign-on with Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="96f1e-151">W portalu Azure na **LMS stanowisko Learning** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-151">In the Azure portal, on the **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="96f1e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="96f1e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="96f1e-155">Na **Learning stanowisko LMS domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="96f1e-155">On the **Learning Seat LMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="96f1e-157">a.</span><span class="sxs-lookup"><span data-stu-id="96f1e-157">a.</span></span> <span data-ttu-id="96f1e-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="96f1e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="96f1e-159">b.</span><span class="sxs-lookup"><span data-stu-id="96f1e-159">b.</span></span> <span data-ttu-id="96f1e-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="96f1e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="96f1e-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="96f1e-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="96f1e-163">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="96f1e-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="96f1e-164">Wartości te nie są wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="96f1e-164">These values are not the real values.</span></span> <span data-ttu-id="96f1e-165">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="96f1e-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="96f1e-166">Skontaktuj się z [zespołem pomocy technicznej stanowisko Learning](http://help.learningseatlms.com/help) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="96f1e-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) to get these values.</span></span> 

5. <span data-ttu-id="96f1e-167">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="96f1e-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="96f1e-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="96f1e-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="96f1e-171">Skonfigurować logowanie jednokrotne w **LMS stanowisko Learning** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej stanowisko Learning](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="96f1e-171">To configure single sign-on on **Learning Seat LMS** side, you need to send the downloaded **Metadata XML** to [Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="96f1e-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="96f1e-172">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="96f1e-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="96f1e-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="96f1e-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96f1e-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96f1e-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f1e-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="96f1e-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="96f1e-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="96f1e-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="96f1e-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="96f1e-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="96f1e-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96f1e-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96f1e-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f1e-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96f1e-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="96f1e-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96f1e-187">a.</span><span class="sxs-lookup"><span data-stu-id="96f1e-187">a.</span></span> <span data-ttu-id="96f1e-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96f1e-189">b.</span><span class="sxs-lookup"><span data-stu-id="96f1e-189">b.</span></span> <span data-ttu-id="96f1e-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="96f1e-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96f1e-191">c.</span><span class="sxs-lookup"><span data-stu-id="96f1e-191">c.</span></span> <span data-ttu-id="96f1e-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="96f1e-193">d.</span><span class="sxs-lookup"><span data-stu-id="96f1e-193">d.</span></span> <span data-ttu-id="96f1e-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="96f1e-195">Tworzenie użytkownika testowego LMS stanowisko Learning</span><span class="sxs-lookup"><span data-stu-id="96f1e-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="96f1e-196">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w LMS stanowisko Learning.</span><span class="sxs-lookup"><span data-stu-id="96f1e-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="96f1e-197">Skontaktuj się z [zespołem pomocy technicznej stanowisko Learning](http://help.learningseatlms.com/help) wszystkie informacje użytkownika, aby dodać użytkowników w aplikacji LMS stanowisko Learning.</span><span class="sxs-lookup"><span data-stu-id="96f1e-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all the user information to add the users in the Learning Seat LMS application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="96f1e-198">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f1e-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="96f1e-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu LMS stanowisko Learning.</span><span class="sxs-lookup"><span data-stu-id="96f1e-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning Seat LMS.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="96f1e-201">**Aby przypisać Simona Britta LMS stanowisko Learning, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="96f1e-201">**To assign Britta Simon to Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="96f1e-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="96f1e-204">Na liście aplikacji zaznacz **LMS stanowisko Learning**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-204">In the applications list, select **Learning Seat LMS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="96f1e-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="96f1e-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="96f1e-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="96f1e-208">Click **Add** button.</span></span> <span data-ttu-id="96f1e-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f1e-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="96f1e-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="96f1e-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="96f1e-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f1e-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96f1e-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f1e-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96f1e-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="96f1e-214">Testing single sign-on</span></span>

<span data-ttu-id="96f1e-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="96f1e-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="96f1e-216">Kliknij Kafelek LMS stanowisko Learning w panelu dostępu, użytkownik będzie można automatycznie zalogowane do aplikacji LMS stanowisko Learning.</span><span class="sxs-lookup"><span data-stu-id="96f1e-216">Click the Learning Seat LMS tile in the Access Panel, you will be automatically signed-on to your Learning Seat LMS application.</span></span> <span data-ttu-id="96f1e-217">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="96f1e-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96f1e-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="96f1e-218">Additional resources</span></span>

* [<span data-ttu-id="96f1e-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96f1e-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96f1e-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96f1e-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

