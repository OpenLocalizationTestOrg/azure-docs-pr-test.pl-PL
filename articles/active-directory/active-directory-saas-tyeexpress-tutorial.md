---
title: 'Samouczek: Integracji Azure Active Directory z T & E Express | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i T & E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 869e5284c71904fcc817ceee0f39d94fab1bc6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="fdef7-103">Samouczek: Integracji Azure Active Directory z T & E Express</span><span class="sxs-lookup"><span data-stu-id="fdef7-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="fdef7-104">Z tego samouczka dowiesz się integrowanie T & E Express z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fdef7-104">In this tutorial, you learn how to integrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fdef7-105">Integracja z usługą Azure AD T & E Express zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="fdef7-105">Integrating T&E Express with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fdef7-106">Można kontrolować w usłudze Azure AD, który ma dostęp do f & E Express</span><span class="sxs-lookup"><span data-stu-id="fdef7-106">You can control in Azure AD who has access to T&E Express</span></span>
- <span data-ttu-id="fdef7-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do f & E Express (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdef7-107">You can enable your users to automatically get signed-on to T&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fdef7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="fdef7-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="fdef7-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fdef7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdef7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fdef7-110">Prerequisites</span></span>

<span data-ttu-id="fdef7-111">Aby skonfigurować integrację usługi Azure AD z T & E Express, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fdef7-111">To configure Azure AD integration with T&E Express, you need the following items:</span></span>

- <span data-ttu-id="fdef7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdef7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fdef7-113">T & E Express jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fdef7-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fdef7-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="fdef7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fdef7-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="fdef7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fdef7-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fdef7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="fdef7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fdef7-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fdef7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="fdef7-118">Scenario description</span></span>
<span data-ttu-id="fdef7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="fdef7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fdef7-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="fdef7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fdef7-121">Dodawanie T & E Express z galerii</span><span class="sxs-lookup"><span data-stu-id="fdef7-121">Adding T&E Express from the gallery</span></span>
2. <span data-ttu-id="fdef7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fdef7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-the-gallery"></a><span data-ttu-id="fdef7-123">Dodawanie T & E Express z galerii</span><span class="sxs-lookup"><span data-stu-id="fdef7-123">Adding T&E Express from the gallery</span></span>
<span data-ttu-id="fdef7-124">Aby skonfigurować integrację T & E Express do usługi Azure AD, należy dodać T & E Express z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="fdef7-124">To configure the integration of T&E Express into Azure AD, you need to add T&E Express from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fdef7-125">**Aby dodać T & E Express z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fdef7-125">**To add T&E Express from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fdef7-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fdef7-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="fdef7-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fdef7-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="fdef7-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fdef7-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="fdef7-133">W polu wyszukiwania wpisz **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-133">In the search box, type **T&E Express**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="fdef7-135">W panelu wyników wybierz **T & E Express**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="fdef7-135">In the results panel, select **T&E Express**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fdef7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fdef7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fdef7-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z T & E Express, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="fdef7-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fdef7-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w T & E Express jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdef7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in T&E Express is to a user in Azure AD.</span></span> <span data-ttu-id="fdef7-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w T & E Express.</span><span class="sxs-lookup"><span data-stu-id="fdef7-140">In other words, a link relationship between an Azure AD user and the related user in T&E Express needs to be established.</span></span>

<span data-ttu-id="fdef7-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **nazwy użytkownika** w T & E Express.</span><span class="sxs-lookup"><span data-stu-id="fdef7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in T&E Express.</span></span>

<span data-ttu-id="fdef7-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z T & E Express, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="fdef7-142">To configure and test Azure AD single sign-on with T&E Express, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fdef7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="fdef7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fdef7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fdef7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fdef7-145">**[Tworzenie użytkownika testowego T & E Express](#creating-a-te-express-test-user)**  — aby mieć odpowiednikiem Simona Britta w T & E Express, która jest połączona z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdef7-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - to have a counterpart of Britta Simon in T&E Express that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="fdef7-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fdef7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fdef7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="fdef7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fdef7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fdef7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fdef7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji T & E Express.</span><span class="sxs-lookup"><span data-stu-id="fdef7-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="fdef7-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z T & E Express, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fdef7-150">**To configure Azure AD single sign-on with T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="fdef7-151">W portalu zarządzania Azure na **T & E Express** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-151">In the Azure Management portal, on the **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="fdef7-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="fdef7-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="fdef7-155">Na **& E Express domeny i adresy URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fdef7-155">On the **T&E Express Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="fdef7-157">a.</span><span class="sxs-lookup"><span data-stu-id="fdef7-157">a.</span></span> <span data-ttu-id="fdef7-158">W **identyfikator** tekstowym, wpisz wartość, jak:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="fdef7-158">In the **Identifier** textbox, type the value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="fdef7-159">b.</span><span class="sxs-lookup"><span data-stu-id="fdef7-159">b.</span></span> <span data-ttu-id="fdef7-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="fdef7-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fdef7-161">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="fdef7-161">Please note that these are not the real values.</span></span> <span data-ttu-id="fdef7-162">Należy zaktualizować te wartości z rzeczywistego identyfikatora i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fdef7-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="fdef7-163">W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="fdef7-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="fdef7-164">Skontaktuj się z [T & E Express obsługują zespołu](http://www.tyeexpress.com/contacto.aspx) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="fdef7-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) to get these values.</span></span>

5. <span data-ttu-id="fdef7-165">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="fdef7-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="fdef7-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fdef7-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fdef7-169">Aby skonfigurować logowanie jednokrotne w **T & E Express** strona, zaloguj się do T & E express aplikacji bez funkcji logowania jednokrotnego SAML przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="fdef7-169">To configure single sign-on on **T&E Express** side, login to the T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="fdef7-170">W obszarze **Admin** kliknij **domeny SAML** aby otworzyć stronę ustawienia SAML.</span><span class="sxs-lookup"><span data-stu-id="fdef7-170">Under the **Admin** Tab, Click on **SAML domain** to Open the SAML settings page.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="fdef7-172">Wybierz **Activar(Activate)** opcję **nr** do **SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-172">Select the **Activar(Activate)** option from **No** to **SI(Yes)**.</span></span> <span data-ttu-id="fdef7-173">W **metadanych dostawcy tożsamości** pole tekstowe, Wklej metadane XML, których donwloaded z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fdef7-173">In the **Identity Provider Metadata** textbox, paste the metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="fdef7-175">Polecenie **Guardar(Save)** przycisk, aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="fdef7-175">Click on the **Guardar(Save)** button to save the settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fdef7-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdef7-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="fdef7-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fdef7-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="fdef7-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fdef7-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fdef7-180">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fdef7-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fdef7-182">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="fdef7-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fdef7-184">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fdef7-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fdef7-186">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fdef7-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fdef7-188">a.</span><span class="sxs-lookup"><span data-stu-id="fdef7-188">a.</span></span> <span data-ttu-id="fdef7-189">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fdef7-190">b.</span><span class="sxs-lookup"><span data-stu-id="fdef7-190">b.</span></span> <span data-ttu-id="fdef7-191">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fdef7-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fdef7-192">c.</span><span class="sxs-lookup"><span data-stu-id="fdef7-192">c.</span></span> <span data-ttu-id="fdef7-193">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fdef7-194">d.</span><span class="sxs-lookup"><span data-stu-id="fdef7-194">d.</span></span> <span data-ttu-id="fdef7-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="fdef7-196">Tworzenie użytkownika testowego T & E Express</span><span class="sxs-lookup"><span data-stu-id="fdef7-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="fdef7-197">Aby włączyć użytkowników usługi Azure AD zalogować się do T & E Express, musi być przygotowana do T & E Express.</span><span class="sxs-lookup"><span data-stu-id="fdef7-197">In order to enable Azure AD users to log into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="fdef7-198">W przypadku T & E Express Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="fdef7-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="fdef7-199">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fdef7-199">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="fdef7-200">Zaloguj się do witryny firmy T & E Express jako administrator.</span><span class="sxs-lookup"><span data-stu-id="fdef7-200">Log in to your T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="fdef7-201">W obszarze tagu administratora kliknij na użytkowników, aby otworzyć stronę wzorcową użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fdef7-201">Under Admin tag, click on Users to open the Users master page.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="fdef7-203">Na stronie głównej kliknij  **+**  Aby dodać użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fdef7-203">On the home page, click on **+** to add the users.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="fdef7-205">Wprowadź wszelkie wymagane informacje, jak zadawane w formularzu i kliknij przycisk Zapisz, aby zapisać szczegóły.</span><span class="sxs-lookup"><span data-stu-id="fdef7-205">Enter all the mandatory details as asked in the form and click the save button to save the details.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Dodawanie pracownika](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fdef7-208">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdef7-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fdef7-209">W tej sekcji można włączyć Simona Britta na udostępnienie jej do f & E Express za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fdef7-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to T&E Express.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="fdef7-211">**Aby przypisać Simona Britta T & E Express, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fdef7-211">**To assign Britta Simon to T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="fdef7-212">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-212">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="fdef7-214">Na liście aplikacji zaznacz **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-214">In the applications list, select **T&E Express**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="fdef7-216">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="fdef7-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="fdef7-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fdef7-218">Click **Add** button.</span></span> <span data-ttu-id="fdef7-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fdef7-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="fdef7-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="fdef7-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fdef7-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fdef7-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fdef7-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fdef7-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fdef7-224">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fdef7-224">Testing single sign-on</span></span>

<span data-ttu-id="fdef7-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="fdef7-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fdef7-226">Po kliknięciu kafelka T & E Express w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji T & E Express.</span><span class="sxs-lookup"><span data-stu-id="fdef7-226">When you click the T&E Express tile in the Access Panel, you should get automatically signed-on to your T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fdef7-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="fdef7-227">Additional resources</span></span>

* [<span data-ttu-id="fdef7-228">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdef7-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fdef7-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fdef7-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

