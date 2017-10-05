---
title: "Samouczek: Integracji Azure Active Directory ze wskazówkami firmy Microsoft | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i wskazówkami w systemie Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f9c068c71eb00a4c779c91c8ee0f0dc9d6ba85ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="4e67e-103">Samouczek: Integracji Azure Active Directory ze wskazówkami firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="4e67e-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="4e67e-104">Z tego samouczka dowiesz sposobu integracji z usługą Azure Active Directory (Azure AD) kierunkach firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e67e-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e67e-105">Integracja z usługą Azure AD instrukcjami w systemie Microsoft zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4e67e-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4e67e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do wskazówek w systemie Microsoft</span><span class="sxs-lookup"><span data-stu-id="4e67e-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="4e67e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do kierunkach firmy Microsoft (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e67e-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e67e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4e67e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4e67e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4e67e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e67e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4e67e-110">Prerequisites</span></span>

<span data-ttu-id="4e67e-111">Aby skonfigurować integrację usługi Azure AD ze wskazówkami firmy Microsoft, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4e67e-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="4e67e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e67e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e67e-113">Wskazówki na Microsoft logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4e67e-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e67e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4e67e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e67e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4e67e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e67e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4e67e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e67e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e67e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e67e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4e67e-118">Scenario description</span></span>
<span data-ttu-id="4e67e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4e67e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e67e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4e67e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e67e-121">Dodawanie kierunki na firmy Microsoft z galerii</span><span class="sxs-lookup"><span data-stu-id="4e67e-121">Adding Directions on Microsoft from the gallery</span></span>
2. <span data-ttu-id="4e67e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4e67e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="4e67e-123">Dodawanie kierunki na firmy Microsoft z galerii</span><span class="sxs-lookup"><span data-stu-id="4e67e-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="4e67e-124">Aby skonfigurować integrację z kierunków firmy Microsoft do usługi Azure AD, należy dodać instrukcjami w systemie Microsoft z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4e67e-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4e67e-125">**Aby dodać instrukcjami w systemie Microsoft z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4e67e-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4e67e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4e67e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4e67e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4e67e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4e67e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4e67e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4e67e-133">W polu wyszukiwania wpisz **kierunkach Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="4e67e-135">W panelu wyników wybierz **kierunkach Microsoft**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="4e67e-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4e67e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4e67e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4e67e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej ze wskazówkami firmy Microsoft na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="4e67e-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4e67e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w kierunkach firmy Microsoft jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e67e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="4e67e-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w kierunkach w systemie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e67e-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="4e67e-141">W kierunkach firmy Microsoft, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="4e67e-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4e67e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej ze wskazówkami firmy Microsoft, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="4e67e-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4e67e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4e67e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4e67e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4e67e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e67e-145">**[Tworzenie kierunki na użytkownika testowego Microsoft](#creating-a-directions-on-microsoft-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta kierunkach firmy Microsoft, który jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4e67e-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e67e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4e67e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e67e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="4e67e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4e67e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4e67e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4e67e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w z instrukcjami w aplikacji Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e67e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="4e67e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej ze wskazówkami firmy Microsoft, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4e67e-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="4e67e-151">W portalu Azure na **kierunkach Microsoft** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4e67e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="4e67e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="4e67e-155">Na **kierunkach adresy URL i Domain Microsoft** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4e67e-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="4e67e-157">a.</span><span class="sxs-lookup"><span data-stu-id="4e67e-157">a.</span></span> <span data-ttu-id="4e67e-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="4e67e-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="4e67e-159">b.</span><span class="sxs-lookup"><span data-stu-id="4e67e-159">b.</span></span> <span data-ttu-id="4e67e-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="4e67e-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="4e67e-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4e67e-161">These values are not real.</span></span> <span data-ttu-id="4e67e-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="4e67e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4e67e-163">Skontaktuj się z [zespołu obsługi kierunkach Microsoft Client](mailto:service@DirectionsOnMicrosoft.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="4e67e-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
4. <span data-ttu-id="4e67e-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4e67e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="4e67e-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4e67e-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4e67e-168">Skonfigurować logowanie jednokrotne w **kierunkach Microsoft** stronie, musisz wysłać pobrany **XML metadanych** do [kierunkach Microsoft obsługują zespołu](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4e67e-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="4e67e-169">Aby włączyć kierunki zespołu pomocy technicznej firmy Microsoft można znaleźć członkostwem w witrynie federacyjnych, obejmują informacje o Twojej firmie w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="4e67e-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="4e67e-170">Logowanie jednokrotne dla kierunków Microsoft musi być włączona przez [kierunkach Microsoft Client obsługuje zespołu](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4e67e-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="4e67e-171">Otrzymasz powiadomienie podczas logowania jednokrotnego została włączona.</span><span class="sxs-lookup"><span data-stu-id="4e67e-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="4e67e-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="4e67e-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4e67e-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="4e67e-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4e67e-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4e67e-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4e67e-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e67e-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="4e67e-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4e67e-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4e67e-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4e67e-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4e67e-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4e67e-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4e67e-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e67e-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4e67e-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e67e-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4e67e-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e67e-187">a.</span><span class="sxs-lookup"><span data-stu-id="4e67e-187">a.</span></span> <span data-ttu-id="4e67e-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e67e-189">b.</span><span class="sxs-lookup"><span data-stu-id="4e67e-189">b.</span></span> <span data-ttu-id="4e67e-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4e67e-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4e67e-191">c.</span><span class="sxs-lookup"><span data-stu-id="4e67e-191">c.</span></span> <span data-ttu-id="4e67e-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4e67e-193">d.</span><span class="sxs-lookup"><span data-stu-id="4e67e-193">d.</span></span> <span data-ttu-id="4e67e-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="4e67e-195">Tworzenie kierunki na użytkownika testowego firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="4e67e-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="4e67e-196">Nie ma elementu akcji do skonfigurowania użytkownika inicjowania obsługi administracyjnej kierunkach firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e67e-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="4e67e-197">Gdy przypisany użytkownik próbuje zalogować się do wskazówek na korzystanie z panelu dostępu firmy Microsoft, kierunkach Microsoft sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="4e67e-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="4e67e-198">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez kierunkach firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e67e-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4e67e-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e67e-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4e67e-200">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu kierunkach firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e67e-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4e67e-202">**Aby przypisać Simona Britta kierunkach firmy Microsoft, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4e67e-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="4e67e-203">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4e67e-205">Na liście aplikacji zaznacz **kierunkach Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="4e67e-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4e67e-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4e67e-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4e67e-209">Click **Add** button.</span></span> <span data-ttu-id="4e67e-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4e67e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4e67e-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="4e67e-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4e67e-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4e67e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e67e-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4e67e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4e67e-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4e67e-215">Testing single sign-on</span></span>

<span data-ttu-id="4e67e-216">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4e67e-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="4e67e-217">Po kliknięciu kierunki na kafelku firmy Microsoft w panelu dostępu należy należy pobrać automatycznie zalogowane się z instrukcjami w aplikacji Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e67e-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="4e67e-218">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4e67e-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4e67e-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4e67e-219">Additional resources</span></span>

* [<span data-ttu-id="4e67e-220">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e67e-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e67e-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4e67e-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

