---
title: 'Samouczek: Integracji Azure Active Directory z Clever | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="07264-103">Samouczek: Integracji Azure Active Directory z Clever</span><span class="sxs-lookup"><span data-stu-id="07264-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="07264-104">Z tego samouczka dowiesz się integrowanie Clever z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07264-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07264-105">Integracja z usługą Azure AD Clever zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="07264-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07264-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Clever.</span><span class="sxs-lookup"><span data-stu-id="07264-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="07264-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Clever (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07264-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="07264-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="07264-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="07264-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07264-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07264-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="07264-110">Prerequisites</span></span>

<span data-ttu-id="07264-111">Aby skonfigurować integrację usługi Azure AD z Clever, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="07264-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="07264-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="07264-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07264-113">Inteligentne logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="07264-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07264-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="07264-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07264-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="07264-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07264-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="07264-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07264-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07264-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07264-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="07264-118">Scenario description</span></span>
<span data-ttu-id="07264-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="07264-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07264-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="07264-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07264-121">Dodawanie Clever z galerii</span><span class="sxs-lookup"><span data-stu-id="07264-121">Adding Clever from the gallery</span></span>
2. <span data-ttu-id="07264-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="07264-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="07264-123">Dodawanie Clever z galerii</span><span class="sxs-lookup"><span data-stu-id="07264-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="07264-124">Aby skonfigurować integrację usługi Azure AD Clever, należy dodać Clever z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="07264-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07264-125">**Aby dodać Clever z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="07264-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07264-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="07264-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="07264-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="07264-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07264-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="07264-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="07264-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="07264-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="07264-133">W polu wyszukiwania wpisz **Clever**, wybierz pozycję **Clever** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="07264-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![Inteligentne z listy wyników](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="07264-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="07264-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="07264-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Clever w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="07264-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07264-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Clever jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07264-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="07264-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Clever musi się.</span><span class="sxs-lookup"><span data-stu-id="07264-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="07264-139">W Clever, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="07264-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="07264-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Clever, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="07264-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07264-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="07264-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07264-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="07264-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07264-143">**[Tworzenie użytkownika testowego inteligentne](#create-a-clever-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Clever połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07264-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07264-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="07264-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07264-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="07264-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="07264-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="07264-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="07264-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w inteligentne aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07264-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="07264-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Clever, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="07264-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="07264-149">W portalu Azure na **Clever** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="07264-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="07264-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="07264-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="07264-153">Na **inteligentne domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="07264-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Inteligentne domeny i adresów URL jednym informacje logowania jednokrotnego](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="07264-155">a.</span><span class="sxs-lookup"><span data-stu-id="07264-155">a.</span></span> <span data-ttu-id="07264-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="07264-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="07264-157">b.</span><span class="sxs-lookup"><span data-stu-id="07264-157">b.</span></span> <span data-ttu-id="07264-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="07264-158">In the **Identifier** textbox, type a URL using the following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="07264-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="07264-159">These values are not real.</span></span> <span data-ttu-id="07264-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="07264-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="07264-161">Skontaktuj się z [zespołem pomocy technicznej klienta inteligentne](https://clever.com/about/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="07264-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get these values.</span></span>

4. <span data-ttu-id="07264-162">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="07264-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="07264-164">Inteligentne aplikacji oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do Twojej **atrybuty tokenu SAML** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="07264-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="07264-165">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="07264-165">The following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="07264-167">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="07264-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="07264-168">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="07264-168">Attribute Name</span></span>  | <span data-ttu-id="07264-169">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="07264-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="07264-170">clever.student.Credentials.District\_nazwy użytkownika</span><span class="sxs-lookup"><span data-stu-id="07264-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="07264-171">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="07264-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="07264-172">Imię</span><span class="sxs-lookup"><span data-stu-id="07264-172">Firstname</span></span>  | <span data-ttu-id="07264-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="07264-173">user.givenname</span></span> |
    | <span data-ttu-id="07264-174">nazwisko</span><span class="sxs-lookup"><span data-stu-id="07264-174">Lastname</span></span>  | <span data-ttu-id="07264-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="07264-175">user.surname</span></span> |    

    <span data-ttu-id="07264-176">a.</span><span class="sxs-lookup"><span data-stu-id="07264-176">a.</span></span> <span data-ttu-id="07264-177">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="07264-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="07264-180">b.</span><span class="sxs-lookup"><span data-stu-id="07264-180">b.</span></span> <span data-ttu-id="07264-181">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="07264-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="07264-182">c.</span><span class="sxs-lookup"><span data-stu-id="07264-182">c.</span></span> <span data-ttu-id="07264-183">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="07264-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="07264-184">d.</span><span class="sxs-lookup"><span data-stu-id="07264-184">d.</span></span> <span data-ttu-id="07264-185">Pozostaw **Namespace** puste pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="07264-185">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="07264-186">d.</span><span class="sxs-lookup"><span data-stu-id="07264-186">d.</span></span> <span data-ttu-id="07264-187">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="07264-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="07264-188">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="07264-188">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="07264-190">Aby wygenerować **metadanych** adres url, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="07264-190">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="07264-191">a.</span><span class="sxs-lookup"><span data-stu-id="07264-191">a.</span></span> <span data-ttu-id="07264-192">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="07264-192">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="07264-194">b.</span><span class="sxs-lookup"><span data-stu-id="07264-194">b.</span></span> <span data-ttu-id="07264-195">Kliknij przycisk **punkty końcowe** otworzyć **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="07264-195">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="07264-197">c.</span><span class="sxs-lookup"><span data-stu-id="07264-197">c.</span></span> <span data-ttu-id="07264-198">Kliknij przycisk Kopiuj, aby skopiować **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="07264-198">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="07264-200">d.</span><span class="sxs-lookup"><span data-stu-id="07264-200">d.</span></span> <span data-ttu-id="07264-201">Teraz przejdź do strony właściwości **Clever** i skopiuj **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="07264-201">Now go to the property page of **Clever** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="07264-203">e.</span><span class="sxs-lookup"><span data-stu-id="07264-203">e.</span></span> <span data-ttu-id="07264-204">Generowanie **adres URL metadanych** przy użyciu następującego wzorca:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="07264-204">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="07264-205">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy inteligentne.</span><span class="sxs-lookup"><span data-stu-id="07264-205">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

10. <span data-ttu-id="07264-206">Na pasku narzędzi, kliknij przycisk **błyskawicznych logowania**.</span><span class="sxs-lookup"><span data-stu-id="07264-206">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="07264-207">![Logowania błyskawicznych](./media/active-directory-saas-clever-tutorial/ic798984.png "błyskawicznych logowania")</span><span class="sxs-lookup"><span data-stu-id="07264-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="07264-208">Na **błyskawicznych logowania** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="07264-208">On the **Instant Login** page, perform the following steps:</span></span>
      
      <span data-ttu-id="07264-209">![Logowania błyskawicznych](./media/active-directory-saas-clever-tutorial/ic798985.png "błyskawicznych logowania")</span><span class="sxs-lookup"><span data-stu-id="07264-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="07264-210">a.</span><span class="sxs-lookup"><span data-stu-id="07264-210">a.</span></span> <span data-ttu-id="07264-211">Typ **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="07264-211">Type the **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="07264-212">**Adres URL logowania** jest niestandardowa wartość.</span><span class="sxs-lookup"><span data-stu-id="07264-212">The **Login URL** is a custom value.</span></span> <span data-ttu-id="07264-213">Skontaktuj się z [zespołem pomocy technicznej klienta inteligentne](https://clever.com/about/contact/) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="07264-213">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
      
      <span data-ttu-id="07264-214">b.</span><span class="sxs-lookup"><span data-stu-id="07264-214">b.</span></span> <span data-ttu-id="07264-215">Jako **systemu tożsamości**, wybierz pozycję **usług AD FS**.</span><span class="sxs-lookup"><span data-stu-id="07264-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="07264-216">c.</span><span class="sxs-lookup"><span data-stu-id="07264-216">c.</span></span> <span data-ttu-id="07264-217">Typ **adres URL metadanych** w **adres URL metadanych** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="07264-217">Type the **Metadata URL** in the **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="07264-218">d.</span><span class="sxs-lookup"><span data-stu-id="07264-218">d.</span></span> <span data-ttu-id="07264-219">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="07264-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="07264-220">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="07264-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07264-221">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="07264-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07264-222">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07264-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="07264-223">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="07264-223">Create an Azure AD test user</span></span>

<span data-ttu-id="07264-224">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="07264-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="07264-226">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="07264-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07264-227">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="07264-227">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="07264-229">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="07264-229">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="07264-231">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="07264-231">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="07264-233">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="07264-233">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="07264-235">a.</span><span class="sxs-lookup"><span data-stu-id="07264-235">a.</span></span> <span data-ttu-id="07264-236">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07264-236">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07264-237">b.</span><span class="sxs-lookup"><span data-stu-id="07264-237">b.</span></span> <span data-ttu-id="07264-238">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="07264-238">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="07264-239">c.</span><span class="sxs-lookup"><span data-stu-id="07264-239">c.</span></span> <span data-ttu-id="07264-240">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="07264-240">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="07264-241">d.</span><span class="sxs-lookup"><span data-stu-id="07264-241">d.</span></span> <span data-ttu-id="07264-242">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="07264-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="07264-243">Tworzenie użytkownika testowego inteligentne</span><span class="sxs-lookup"><span data-stu-id="07264-243">Create a Clever test user</span></span>

<span data-ttu-id="07264-244">Aby umożliwić użytkownikom usługi Azure AD zalogować się do Clever, musi być przygotowana do Clever.</span><span class="sxs-lookup"><span data-stu-id="07264-244">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="07264-245">W przypadku Clever, Praca z [zespołem pomocy technicznej klienta inteligentne](https://clever.com/about/contact/) Aby dodać użytkowników do platformy inteligentne.</span><span class="sxs-lookup"><span data-stu-id="07264-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="07264-246">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="07264-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="07264-247">Możesz użyć innych inteligentne użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Clever do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07264-247">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="07264-248">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="07264-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="07264-249">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Clever.</span><span class="sxs-lookup"><span data-stu-id="07264-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="07264-251">**Aby przypisać Simona Britta Clever, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="07264-251">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="07264-252">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="07264-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="07264-254">Na liście aplikacji zaznacz **Clever**.</span><span class="sxs-lookup"><span data-stu-id="07264-254">In the applications list, select **Clever**.</span></span>

    ![Clever łącza na liście aplikacji](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="07264-256">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="07264-256">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="07264-258">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="07264-258">Click **Add** button.</span></span> <span data-ttu-id="07264-259">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="07264-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="07264-261">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="07264-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07264-262">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="07264-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07264-263">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="07264-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="07264-264">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="07264-264">Test single sign-on</span></span>

<span data-ttu-id="07264-265">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="07264-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="07264-266">Po kliknięciu kafelka inteligentne w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane inteligentne aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07264-266">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="07264-267">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07264-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="07264-268">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="07264-268">Additional resources</span></span>

* [<span data-ttu-id="07264-269">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07264-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07264-270">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07264-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

