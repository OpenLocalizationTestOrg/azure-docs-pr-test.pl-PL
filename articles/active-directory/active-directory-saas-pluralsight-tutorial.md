---
title: 'Samouczek: Integracji Azure Active Directory z Pluralsight | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 62429643a108665544e42001d264046b5db1ec97
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="dbf27-103">Samouczek: Integracji Azure Active Directory z Pluralsight</span><span class="sxs-lookup"><span data-stu-id="dbf27-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="dbf27-104">Z tego samouczka dowiesz się integrowanie Pluralsight z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dbf27-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dbf27-105">Integracja z usługą Azure AD Pluralsight zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="dbf27-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dbf27-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Pluralsight</span><span class="sxs-lookup"><span data-stu-id="dbf27-106">You can control in Azure AD who has access to Pluralsight</span></span>
- <span data-ttu-id="dbf27-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Pluralsight (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbf27-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dbf27-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dbf27-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dbf27-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dbf27-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbf27-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dbf27-110">Prerequisites</span></span>

<span data-ttu-id="dbf27-111">Aby skonfigurować integrację usługi Azure AD z Pluralsight, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="dbf27-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

- <span data-ttu-id="dbf27-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbf27-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dbf27-113">Pluralsight logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="dbf27-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dbf27-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="dbf27-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dbf27-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="dbf27-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dbf27-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="dbf27-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dbf27-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbf27-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dbf27-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="dbf27-118">Scenario description</span></span>
<span data-ttu-id="dbf27-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="dbf27-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dbf27-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="dbf27-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dbf27-121">Dodawanie Pluralsight z galerii</span><span class="sxs-lookup"><span data-stu-id="dbf27-121">Adding Pluralsight from the gallery</span></span>
2. <span data-ttu-id="dbf27-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="dbf27-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-the-gallery"></a><span data-ttu-id="dbf27-123">Dodawanie Pluralsight z galerii</span><span class="sxs-lookup"><span data-stu-id="dbf27-123">Adding Pluralsight from the gallery</span></span>
<span data-ttu-id="dbf27-124">Aby skonfigurować integrację Pluralsight do usługi Azure AD, należy dodać Pluralsight z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="dbf27-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dbf27-125">**Aby dodać Pluralsight z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dbf27-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dbf27-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dbf27-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="dbf27-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dbf27-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="dbf27-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dbf27-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="dbf27-133">W polu wyszukiwania wpisz **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-133">In the search box, type **Pluralsight**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="dbf27-135">W panelu wyników wybierz **Pluralsight**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="dbf27-135">In the results panel, select **Pluralsight**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dbf27-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="dbf27-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dbf27-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pluralsight w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="dbf27-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dbf27-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w Pluralsight do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbf27-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span></span> <span data-ttu-id="dbf27-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Pluralsight musi się.</span><span class="sxs-lookup"><span data-stu-id="dbf27-140">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span></span>

<span data-ttu-id="dbf27-141">W Pluralsight, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="dbf27-141">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dbf27-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pluralsight, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="dbf27-142">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dbf27-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="dbf27-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dbf27-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dbf27-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dbf27-145">**[Tworzenie użytkownika testowego Pluralsight](#creating-a-pluralsight-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Pluralsight połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dbf27-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dbf27-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dbf27-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dbf27-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="dbf27-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dbf27-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dbf27-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dbf27-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="dbf27-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="dbf27-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Pluralsight, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dbf27-150">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="dbf27-151">W portalu Azure na **Pluralsight** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-151">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="dbf27-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="dbf27-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="dbf27-155">Na **Pluralsight domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dbf27-155">On the **Pluralsight Domain and URLs** section, perform the following:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="dbf27-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="dbf27-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dbf27-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="dbf27-158">This value is not real.</span></span> <span data-ttu-id="dbf27-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="dbf27-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="dbf27-160">Skontaktuj się z [zespołem pomocy technicznej klienta Pluralsight](mailto:support@pluralsight.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="dbf27-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get this value.</span></span> 
 


4. <span data-ttu-id="dbf27-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dbf27-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="dbf27-163">Celem tej sekcji jest można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfiguruj logowanie Jednokrotne w aplikacji Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="dbf27-163">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span></span>

    <span data-ttu-id="dbf27-164">Aplikacja Pluralsight oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="dbf27-164">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="dbf27-165">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="dbf27-165">The following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="dbf27-167">Można również dodać **"Unikatowy identyfikator"** atrybutu odpowiednią wartość jak identyfikator pracownika lub inny element, który jest odpowiedni dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="dbf27-167">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="dbf27-168">Należy również zauważyć, że nie jest wymagany atrybut; można jednak dodać go do identyfikowania użytkownika unikatowy.</span><span class="sxs-lookup"><span data-stu-id="dbf27-168">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

6. <span data-ttu-id="dbf27-169">Aby dodać wymagane **atrybuty tokenu SAML**, dla każdego wiersza w tabeli poniżej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dbf27-169">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="dbf27-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="dbf27-170">Attribute Name</span></span> | <span data-ttu-id="dbf27-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="dbf27-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="dbf27-172">Imię</span><span class="sxs-lookup"><span data-stu-id="dbf27-172">First Name</span></span> |<span data-ttu-id="dbf27-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="dbf27-173">user.givenname</span></span> |
   | <span data-ttu-id="dbf27-174">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="dbf27-174">Last Name</span></span> |<span data-ttu-id="dbf27-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="dbf27-175">user.surname</span></span> |
   | <span data-ttu-id="dbf27-176">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="dbf27-176">Email</span></span> |<span data-ttu-id="dbf27-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="dbf27-177">user.mail</span></span> |
   
   <span data-ttu-id="dbf27-178">a.</span><span class="sxs-lookup"><span data-stu-id="dbf27-178">a.</span></span> <span data-ttu-id="dbf27-179">Kliknij przycisk **Dodaj atrybut użytkownika** otworzyć **Dodaj użytkownika Attribure** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dbf27-179">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="dbf27-181">b.</span><span class="sxs-lookup"><span data-stu-id="dbf27-181">b.</span></span> <span data-ttu-id="dbf27-182">W **nazwa atrybutu** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="dbf27-182">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  
   <span data-ttu-id="dbf27-183">c.</span><span class="sxs-lookup"><span data-stu-id="dbf27-183">c.</span></span> <span data-ttu-id="dbf27-184">Z **wartość atrybutu** listy, wybierz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="dbf27-184">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
  
   <span data-ttu-id="dbf27-185">d.</span><span class="sxs-lookup"><span data-stu-id="dbf27-185">d.</span></span> <span data-ttu-id="dbf27-186">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="dbf27-187">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dbf27-187">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="dbf27-189">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [Pluralsight Professional usług](mailTo:professionalservices@pluralsight.com) zespołu i określ plik metadanych pobranych.</span><span class="sxs-lookup"><span data-stu-id="dbf27-189">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="dbf27-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="dbf27-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dbf27-191">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="dbf27-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dbf27-192">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dbf27-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dbf27-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbf27-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="dbf27-194">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dbf27-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="dbf27-196">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dbf27-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dbf27-197">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dbf27-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dbf27-199">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dbf27-201">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dbf27-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dbf27-203">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dbf27-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dbf27-205">a.</span><span class="sxs-lookup"><span data-stu-id="dbf27-205">a.</span></span> <span data-ttu-id="dbf27-206">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dbf27-207">b.</span><span class="sxs-lookup"><span data-stu-id="dbf27-207">b.</span></span> <span data-ttu-id="dbf27-208">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dbf27-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dbf27-209">c.</span><span class="sxs-lookup"><span data-stu-id="dbf27-209">c.</span></span> <span data-ttu-id="dbf27-210">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dbf27-211">d.</span><span class="sxs-lookup"><span data-stu-id="dbf27-211">d.</span></span> <span data-ttu-id="dbf27-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="dbf27-213">Tworzenie użytkownika testowego Pluralsight</span><span class="sxs-lookup"><span data-stu-id="dbf27-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="dbf27-214">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="dbf27-214">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="dbf27-215">We współpracy z [zespołem pomocy technicznej klienta Pluralsight](mailto:support@pluralsight.com) Aby dodać użytkowników w ramach konta Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="dbf27-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dbf27-216">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbf27-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dbf27-217">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="dbf27-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="dbf27-219">**Aby przypisać Simona Britta Pluralsight, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dbf27-219">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="dbf27-220">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="dbf27-222">Na liście aplikacji zaznacz **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-222">In the applications list, select **Pluralsight**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="dbf27-224">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="dbf27-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="dbf27-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dbf27-226">Click **Add** button.</span></span> <span data-ttu-id="dbf27-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dbf27-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="dbf27-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="dbf27-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dbf27-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dbf27-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dbf27-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dbf27-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dbf27-232">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dbf27-232">Testing single sign-on</span></span>

<span data-ttu-id="dbf27-233">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dbf27-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dbf27-234">Po kliknięciu kafelka Pluralsight w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="dbf27-234">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span> <span data-ttu-id="dbf27-235">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dbf27-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dbf27-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="dbf27-236">Additional resources</span></span>

* [<span data-ttu-id="dbf27-237">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dbf27-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dbf27-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dbf27-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

