---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem OfficeSpace | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między oprogramowaniem OfficeSpace i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 43d2ecfe851d8f6c43cd4ce7fc4bd872818f4137
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="a9ca6-103">Samouczek: Azure Active Directory integracji z oprogramowaniem OfficeSpace</span><span class="sxs-lookup"><span data-stu-id="a9ca6-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="a9ca6-104">Z tego samouczka dowiesz się integrowanie OfficeSpace oprogramowania z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9ca6-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9ca6-105">Integracja oprogramowania OfficeSpace z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a9ca6-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9ca6-106">Można kontrolować w usłudze Azure AD, który ma dostęp do oprogramowania OfficeSpace.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-106">You can control in Azure AD who has access to OfficeSpace Software.</span></span>
- <span data-ttu-id="a9ca6-107">Umożliwia użytkownikom automatycznie pobrać zalogowane oprogramowania OfficeSpace (logowanie jednokrotne) z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a9ca6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a9ca6-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a9ca6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9ca6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a9ca6-110">Prerequisites</span></span>

<span data-ttu-id="a9ca6-111">Aby skonfigurować integrację usługi Azure AD z oprogramowaniem OfficeSpace, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a9ca6-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span></span>

- <span data-ttu-id="a9ca6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9ca6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9ca6-113">Oprogramowanie OfficeSpace logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a9ca6-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9ca6-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9ca6-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a9ca6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9ca6-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9ca6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9ca6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9ca6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a9ca6-118">Scenario description</span></span>
<span data-ttu-id="a9ca6-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9ca6-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a9ca6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9ca6-121">Dodawanie oprogramowania OfficeSpace z galerii</span><span class="sxs-lookup"><span data-stu-id="a9ca6-121">Adding OfficeSpace Software from the gallery</span></span>
2. <span data-ttu-id="a9ca6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a9ca6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-the-gallery"></a><span data-ttu-id="a9ca6-123">Dodawanie oprogramowania OfficeSpace z galerii</span><span class="sxs-lookup"><span data-stu-id="a9ca6-123">Adding OfficeSpace Software from the gallery</span></span>
<span data-ttu-id="a9ca6-124">Aby skonfigurować integrację usługi Azure AD OfficeSpace oprogramowania, należy dodać OfficeSpace oprogramowania z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9ca6-125">**Aby dodać OfficeSpace oprogramowanie z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a9ca6-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a9ca6-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="a9ca6-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a9ca6-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="a9ca6-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="a9ca6-133">W polu wyszukiwania wpisz **oprogramowania OfficeSpace**, wybierz pozycję **oprogramowania OfficeSpace** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-133">In the search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button to add the application.</span></span>

    ![OfficeSpace oprogramowania z listy wyników](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a9ca6-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a9ca6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a9ca6-136">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z oprogramowaniem OfficeSpace w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9ca6-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w oprogramowaniu OfficeSpace jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span></span> <span data-ttu-id="a9ca6-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w oprogramowaniu OfficeSpace musi określone.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-138">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span></span>

<span data-ttu-id="a9ca6-139">W oprogramowaniu OfficeSpace, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-139">In OfficeSpace Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a9ca6-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem OfficeSpace, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="a9ca6-140">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a9ca6-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a9ca6-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a9ca6-143">**[Tworzenie użytkownika testowego oprogramowania OfficeSpace](#create-a-officespace-software-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta OfficeSpace oprogramowania, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a9ca6-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a9ca6-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a9ca6-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a9ca6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a9ca6-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w używanej aplikacji OfficeSpace.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="a9ca6-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem OfficeSpace, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a9ca6-148">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="a9ca6-149">W portalu Azure na **oprogramowania OfficeSpace** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-149">In the Azure portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="a9ca6-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="a9ca6-153">Na **OfficeSpace oprogramowania domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a9ca6-153">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny oprogramowania OfficeSpace pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="a9ca6-155">a.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-155">a.</span></span> <span data-ttu-id="a9ca6-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="a9ca6-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="a9ca6-157">b.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-157">b.</span></span> <span data-ttu-id="a9ca6-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="a9ca6-158">In the **Identifier** textbox, type a URL using the following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a9ca6-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-159">These values are not real.</span></span> <span data-ttu-id="a9ca6-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a9ca6-161">Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania OfficeSpace](mailto:support@officespacesoftware.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) to get these values.</span></span> 

4. <span data-ttu-id="a9ca6-162">Aplikacja OfficeSpace oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-162">OfficeSpace Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a9ca6-163">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="a9ca6-164">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a9ca6-165">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-165">The following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie atrybutów](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="a9ca6-167">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okno dialogowe, wybierz opcję **user.mail** jako **identyfikator użytkownika** i dla każdego wiersza w tabeli poniżej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a9ca6-167">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="a9ca6-168">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="a9ca6-168">Attribute Name</span></span> | <span data-ttu-id="a9ca6-169">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="a9ca6-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="a9ca6-170">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="a9ca6-170">email</span></span> | <span data-ttu-id="a9ca6-171">User.mail</span><span class="sxs-lookup"><span data-stu-id="a9ca6-171">user.mail</span></span> |
    | <span data-ttu-id="a9ca6-172">name</span><span class="sxs-lookup"><span data-stu-id="a9ca6-172">name</span></span> | <span data-ttu-id="a9ca6-173">User.DisplayName</span><span class="sxs-lookup"><span data-stu-id="a9ca6-173">user.displayname</span></span> |
    | <span data-ttu-id="a9ca6-174">Imię</span><span class="sxs-lookup"><span data-stu-id="a9ca6-174">first_name</span></span> | <span data-ttu-id="a9ca6-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="a9ca6-175">user.givenname</span></span> |
    | <span data-ttu-id="a9ca6-176">nazwisko</span><span class="sxs-lookup"><span data-stu-id="a9ca6-176">last_name</span></span> | <span data-ttu-id="a9ca6-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="a9ca6-177">user.surname</span></span> |

    <span data-ttu-id="a9ca6-178">a.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-178">a.</span></span> <span data-ttu-id="a9ca6-179">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="a9ca6-180">Skonfiguruj Dodaj</span><span class="sxs-lookup"><span data-stu-id="a9ca6-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie atrybutów](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="a9ca6-182">b.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-182">b.</span></span> <span data-ttu-id="a9ca6-183">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="a9ca6-184">c.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-184">c.</span></span> <span data-ttu-id="a9ca6-185">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a9ca6-186">d.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-186">d.</span></span> <span data-ttu-id="a9ca6-187">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="a9ca6-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="a9ca6-188">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-188">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of the certificate.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="a9ca6-190">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-190">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a9ca6-192">Na **konfiguracji oprogramowania OfficeSpace** , kliknij przycisk **Konfigurowanie oprogramowania OfficeSpace** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-192">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a9ca6-193">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="a9ca6-193">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja oprogramowania OfficeSpace](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="a9ca6-195">W oknie przeglądarki innej witryny sieci web Zaloguj się do dzierżawy OfficeSpace oprogramowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="a9ca6-196">Przejdź do **ustawienia** i kliknij przycisk **łączniki**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-196">Go to **Settings** and click **Connectors**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="a9ca6-198">Kliknij przycisk **uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-198">Click **SAML Authentication**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="a9ca6-200">W **uwierzytelnianie SAML** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a9ca6-200">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="a9ca6-202">a.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-202">a.</span></span> <span data-ttu-id="a9ca6-203">W **adres url wylogowania dostawcy** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-203">In the **Logout provider url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a9ca6-204">b.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-204">b.</span></span> <span data-ttu-id="a9ca6-205">W **klienta idp docelowy adres url** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-205">In the **Client idp target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a9ca6-206">c.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-206">c.</span></span> <span data-ttu-id="a9ca6-207">Wklej **odcisk palca** wartość, która została skopiowana z portalu Azure do **odcisk palca certyfikatu klienta IDP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-207">Paste the **Thumbprint** value which you have copied from Azure portal, into the **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="a9ca6-208">d.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-208">d.</span></span> <span data-ttu-id="a9ca6-209">Kliknij przycisk **Zapisz ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="a9ca6-210">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="a9ca6-210">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a9ca6-211">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-211">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a9ca6-212">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9ca6-212">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a9ca6-213">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9ca6-213">Create an Azure AD test user</span></span>

<span data-ttu-id="a9ca6-214">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="a9ca6-216">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a9ca6-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a9ca6-217">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-217">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a9ca6-219">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-219">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a9ca6-221">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-221">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a9ca6-223">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a9ca6-223">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a9ca6-225">a.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-225">a.</span></span> <span data-ttu-id="a9ca6-226">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9ca6-227">b.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-227">b.</span></span> <span data-ttu-id="a9ca6-228">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-228">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a9ca6-229">c.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-229">c.</span></span> <span data-ttu-id="a9ca6-230">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a9ca6-231">d.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-231">d.</span></span> <span data-ttu-id="a9ca6-232">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="a9ca6-233">Tworzenie użytkownika testowego OfficeSpace oprogramowania</span><span class="sxs-lookup"><span data-stu-id="a9ca6-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="a9ca6-234">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta OfficeSpace oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="a9ca6-235">Oprogramowanie OfficeSpace obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a9ca6-236">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-236">There is no action item for you in this section.</span></span> <span data-ttu-id="a9ca6-237">Nowy użytkownik zostanie utworzony podczas próby dostępu do oprogramowania OfficeSpace, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="a9ca6-238">Jeśli trzeba ręcznie utworzyć użytkownika, musisz skontaktuj się z [zespołem pomocy technicznej oprogramowania OfficeSpace](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="a9ca6-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a9ca6-239">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9ca6-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="a9ca6-240">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do oprogramowania OfficeSpace.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OfficeSpace Software.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="a9ca6-242">**Aby przypisać Simona Britta OfficeSpace oprogramowania, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a9ca6-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="a9ca6-243">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a9ca6-245">Na liście aplikacji zaznacz **oprogramowania OfficeSpace**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-245">In the applications list, select **OfficeSpace Software**.</span></span>

    ![Łącze OfficeSpace oprogramowania na liście aplikacji](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="a9ca6-247">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="a9ca6-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-249">Click **Add** button.</span></span> <span data-ttu-id="a9ca6-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="a9ca6-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a9ca6-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a9ca6-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a9ca6-255">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a9ca6-255">Test single sign-on</span></span>

<span data-ttu-id="a9ca6-256">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a9ca6-257">Po kliknięciu kafelka oprogramowania OfficeSpace w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji oprogramowania OfficeSpace.</span><span class="sxs-lookup"><span data-stu-id="a9ca6-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9ca6-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a9ca6-258">Additional resources</span></span>

* [<span data-ttu-id="a9ca6-259">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9ca6-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a9ca6-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9ca6-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

