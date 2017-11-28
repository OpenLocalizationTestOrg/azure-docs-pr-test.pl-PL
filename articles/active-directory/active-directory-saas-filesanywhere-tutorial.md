---
title: 'Samouczek: Integracji Azure Active Directory z FilesAnywhere | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 4153056bd21006061c6ad8ff9cf3c17de9248628
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="93258-103">Samouczek: Integracji Azure Active Directory z FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="93258-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="93258-104">Z tego samouczka dowiesz się integrowanie FilesAnywhere z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93258-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93258-105">Integracja z usługą Azure AD FilesAnywhere zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="93258-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="93258-106">Można kontrolować w usłudze Azure AD, który ma dostęp do FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="93258-106">You can control in Azure AD who has access to FilesAnywhere</span></span>
- <span data-ttu-id="93258-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do FilesAnywhere (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="93258-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93258-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="93258-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="93258-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93258-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93258-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="93258-110">Prerequisites</span></span>

<span data-ttu-id="93258-111">Aby skonfigurować integrację usługi Azure AD z FilesAnywhere, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="93258-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span></span>

- <span data-ttu-id="93258-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="93258-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93258-113">FilesAnywhere jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="93258-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="93258-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="93258-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="93258-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="93258-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93258-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="93258-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="93258-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93258-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="93258-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="93258-118">Scenario description</span></span>
<span data-ttu-id="93258-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="93258-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93258-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="93258-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93258-121">Dodawanie FilesAnywhere z galerii</span><span class="sxs-lookup"><span data-stu-id="93258-121">Adding FilesAnywhere from the gallery</span></span>
2. <span data-ttu-id="93258-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="93258-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-the-gallery"></a><span data-ttu-id="93258-123">Dodawanie FilesAnywhere z galerii</span><span class="sxs-lookup"><span data-stu-id="93258-123">Adding FilesAnywhere from the gallery</span></span>
<span data-ttu-id="93258-124">Aby skonfigurować integrację usługi Azure AD FilesAnywhere, należy dodać FilesAnywhere z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="93258-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="93258-125">**Aby dodać FilesAnywhere z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="93258-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="93258-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="93258-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="93258-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="93258-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="93258-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="93258-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="93258-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="93258-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="93258-133">W polu wyszukiwania wpisz **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="93258-133">In the search box, type **FilesAnywhere**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="93258-135">W panelu wyników wybierz **FilesAnywhere**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="93258-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93258-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="93258-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93258-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FilesAnywhere w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="93258-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="93258-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w FilesAnywhere jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93258-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span></span> <span data-ttu-id="93258-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w FilesAnywhere musi się.</span><span class="sxs-lookup"><span data-stu-id="93258-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span></span>

<span data-ttu-id="93258-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="93258-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="93258-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FilesAnywhere, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="93258-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="93258-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="93258-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="93258-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="93258-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93258-145">**[Tworzenie użytkownika testowego FilesAnywhere](#creating-a-filesanywhere-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta FilesAnywhere połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93258-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span></span>
3. <span data-ttu-id="93258-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="93258-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="93258-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="93258-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93258-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="93258-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93258-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="93258-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="93258-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z FilesAnywhere, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="93258-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="93258-151">W portalu zarządzania Azure na **FilesAnywhere** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="93258-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="93258-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="93258-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="93258-155">Na **FilesAnywhere domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP zainicjował tryb**:</span><span class="sxs-lookup"><span data-stu-id="93258-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="93258-157">a.</span><span class="sxs-lookup"><span data-stu-id="93258-157">a.</span></span> <span data-ttu-id="93258-158">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="93258-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="93258-159">Należy pamiętać, że wartość **215** jest **clientid** i jest tylko przykładowe.</span><span class="sxs-lookup"><span data-stu-id="93258-159">Please note that the value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="93258-160">Należy zastąpić wartość rzeczywista clientid.</span><span class="sxs-lookup"><span data-stu-id="93258-160">You need to replace it with the actual clientid value.</span></span>

4. <span data-ttu-id="93258-161">Na **FilesAnywhere domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **SP zainicjował tryb**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93258-161">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="93258-163">a.</span><span class="sxs-lookup"><span data-stu-id="93258-163">a.</span></span> <span data-ttu-id="93258-164">Polecenie **Pokaż zaawansowane ustawienia adresu URL** opcji</span><span class="sxs-lookup"><span data-stu-id="93258-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="93258-165">b.</span><span class="sxs-lookup"><span data-stu-id="93258-165">b.</span></span> <span data-ttu-id="93258-166">W **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="93258-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="93258-167">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="93258-167">Please note that these are not the real values.</span></span> <span data-ttu-id="93258-168">Należy zaktualizować te wartości rzeczywistych na adres URL logowania i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="93258-168">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="93258-169">Skontaktuj się z [zespołem pomocy technicznej FilesAnywhere](mailto:support@FilesAnywhere.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="93258-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span></span> 

5. <span data-ttu-id="93258-170">Aplikacja FilesAnywhere oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="93258-170">FilesAnywhere Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="93258-171">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="93258-171">Please configure the following claims for this application.</span></span> <span data-ttu-id="93258-172">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="93258-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="93258-173">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="93258-173">The following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="93258-175">Gdy użytkownicy zarejestrowaniu z FilesAnywhere otrzymują wartość **clientid** atrybutu z [zespołu FilesAnywhere](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="93258-175">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="93258-176">Należy dodać atrybut "Identyfikator klienta" z unikatowych wartości dostarczone przez FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="93258-176">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="93258-177">Te atrybuty pokazanym powyżej są wymagane.</span><span class="sxs-lookup"><span data-stu-id="93258-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="93258-178">Należy pamiętać, że wartość **2331** z **clientid** jest tylko przykładowe.</span><span class="sxs-lookup"><span data-stu-id="93258-178">Please note that the value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="93258-179">Należy podać rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="93258-179">You need to provide the actual value.</span></span>


6. <span data-ttu-id="93258-180">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93258-180">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="93258-181">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="93258-181">Attribute Name</span></span> | <span data-ttu-id="93258-182">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="93258-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="93258-183">ClientID</span><span class="sxs-lookup"><span data-stu-id="93258-183">clientid</span></span> | <span data-ttu-id="93258-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="93258-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="93258-185">a.</span><span class="sxs-lookup"><span data-stu-id="93258-185">a.</span></span> <span data-ttu-id="93258-186">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="93258-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="93258-189">b.</span><span class="sxs-lookup"><span data-stu-id="93258-189">b.</span></span> <span data-ttu-id="93258-190">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="93258-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="93258-191">c.</span><span class="sxs-lookup"><span data-stu-id="93258-191">c.</span></span> <span data-ttu-id="93258-192">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="93258-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="93258-193">d.</span><span class="sxs-lookup"><span data-stu-id="93258-193">d.</span></span> <span data-ttu-id="93258-194">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="93258-194">Click **Ok**</span></span>

7. <span data-ttu-id="93258-195">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="93258-195">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="93258-197">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="93258-197">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="93258-199">Na **konfiguracji FilesAnywhere** , kliknij przycisk **skonfigurować FilesAnywhere** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="93258-199">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="93258-202">Aby uzyskać pełną konfiguracji logowania jednokrotnego dla aplikacji na końcu FilesAnywhere, skontaktuj się z [zespołem pomocy technicznej FilesAnywhere](mailto:support@FilesAnywhere.com) i podaj pobrany tokenu SAML podpisywania certyfikatu i jednego znaku w rejestracji jednokrotnej (SSO) adres URL.</span><span class="sxs-lookup"><span data-stu-id="93258-202">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93258-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="93258-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="93258-204">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="93258-204">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="93258-206">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="93258-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="93258-207">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="93258-207">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93258-209">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="93258-209">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93258-211">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="93258-211">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93258-213">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93258-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93258-215">a.</span><span class="sxs-lookup"><span data-stu-id="93258-215">a.</span></span> <span data-ttu-id="93258-216">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93258-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93258-217">b.</span><span class="sxs-lookup"><span data-stu-id="93258-217">b.</span></span> <span data-ttu-id="93258-218">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="93258-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93258-219">c.</span><span class="sxs-lookup"><span data-stu-id="93258-219">c.</span></span> <span data-ttu-id="93258-220">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="93258-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="93258-221">d.</span><span class="sxs-lookup"><span data-stu-id="93258-221">d.</span></span> <span data-ttu-id="93258-222">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="93258-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="93258-223">Tworzenie użytkownika testowego FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="93258-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="93258-224">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji automatycznie.</span><span class="sxs-lookup"><span data-stu-id="93258-224">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="93258-225">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="93258-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="93258-226">W tej sekcji można włączyć Simona Britta do udostępnienia jej FilesAnywhere za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="93258-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="93258-228">**Aby przypisać Simona Britta FilesAnywhere, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="93258-228">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="93258-229">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="93258-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="93258-231">Na liście aplikacji zaznacz **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="93258-231">In the applications list, select **FilesAnywhere**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="93258-233">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="93258-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="93258-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="93258-235">Click **Add** button.</span></span> <span data-ttu-id="93258-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="93258-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="93258-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="93258-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="93258-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="93258-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93258-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="93258-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="93258-241">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="93258-241">Testing single sign-on</span></span>

<span data-ttu-id="93258-242">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="93258-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="93258-243">Po kliknięciu kafelka FilesAnywhere w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="93258-243">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="93258-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="93258-244">Additional resources</span></span>

* [<span data-ttu-id="93258-245">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93258-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93258-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="93258-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
