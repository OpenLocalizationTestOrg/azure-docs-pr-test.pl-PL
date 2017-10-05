---
title: 'Samouczek: Integracji Azure Active Directory z BetterWorks | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i BetterWorks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="d0f97-103">Samouczek: Integracji Azure Active Directory z BetterWorks</span><span class="sxs-lookup"><span data-stu-id="d0f97-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="d0f97-104">Z tego samouczka dowiesz się integrowanie BetterWorks z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0f97-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0f97-105">Integracja z usługą Azure AD BetterWorks zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d0f97-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d0f97-106">Można kontrolować w usłudze Azure AD, który ma dostęp do BetterWorks</span><span class="sxs-lookup"><span data-stu-id="d0f97-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="d0f97-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do BetterWorks (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f97-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0f97-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d0f97-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d0f97-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0f97-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0f97-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d0f97-110">Prerequisites</span></span>

<span data-ttu-id="d0f97-111">Aby skonfigurować integrację usługi Azure AD z BetterWorks, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d0f97-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="d0f97-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f97-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0f97-113">BetterWorks jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d0f97-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0f97-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d0f97-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0f97-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d0f97-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0f97-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d0f97-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0f97-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0f97-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0f97-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d0f97-118">Scenario description</span></span>
<span data-ttu-id="d0f97-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d0f97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0f97-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d0f97-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0f97-121">Dodawanie BetterWorks z galerii</span><span class="sxs-lookup"><span data-stu-id="d0f97-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="d0f97-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d0f97-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="d0f97-123">Dodawanie BetterWorks z galerii</span><span class="sxs-lookup"><span data-stu-id="d0f97-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="d0f97-124">Aby skonfigurować integrację usługi Azure AD BetterWorks, należy dodać BetterWorks z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d0f97-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d0f97-125">**Aby dodać BetterWorks z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d0f97-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d0f97-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d0f97-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d0f97-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d0f97-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d0f97-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0f97-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d0f97-133">W polu wyszukiwania wpisz **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-133">In the search box, type **BetterWorks**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="d0f97-135">W panelu wyników wybierz **BetterWorks**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d0f97-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0f97-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d0f97-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0f97-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BetterWorks na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d0f97-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d0f97-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w BetterWorks jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0f97-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="d0f97-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w BetterWorks musi się.</span><span class="sxs-lookup"><span data-stu-id="d0f97-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="d0f97-141">W BetterWorks, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="d0f97-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d0f97-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BetterWorks, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="d0f97-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d0f97-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d0f97-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d0f97-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d0f97-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0f97-145">**[Tworzenie użytkownika testowego BetterWorks](#creating-a-betterworks-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta BetterWorks połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d0f97-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0f97-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d0f97-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0f97-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="d0f97-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0f97-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d0f97-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0f97-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="d0f97-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="d0f97-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z BetterWorks, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d0f97-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="d0f97-151">W portalu Azure na **BetterWorks** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d0f97-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="d0f97-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="d0f97-155">Na **BetterWorks domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP zainicjował tryb**:</span><span class="sxs-lookup"><span data-stu-id="d0f97-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="d0f97-157">a.</span><span class="sxs-lookup"><span data-stu-id="d0f97-157">a.</span></span> <span data-ttu-id="d0f97-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="d0f97-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="d0f97-159">b.</span><span class="sxs-lookup"><span data-stu-id="d0f97-159">b.</span></span> <span data-ttu-id="d0f97-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="d0f97-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="d0f97-161">Na **BetterWorks domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **SP zainicjował tryb**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d0f97-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="d0f97-163">a.</span><span class="sxs-lookup"><span data-stu-id="d0f97-163">a.</span></span> <span data-ttu-id="d0f97-164">Polecenie **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="d0f97-165">b.</span><span class="sxs-lookup"><span data-stu-id="d0f97-165">b.</span></span> <span data-ttu-id="d0f97-166">W **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="d0f97-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d0f97-167">Nie są to rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="d0f97-167">These are not real values.</span></span> <span data-ttu-id="d0f97-168">Adres URL odpowiedzi, identyfikator i rzeczywistych na adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="d0f97-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="d0f97-169">Skontaktuj się z [BetterWorks obsługuje zespołu](mailto:support@betterworks.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="d0f97-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="d0f97-170">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d0f97-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="d0f97-172">Aplikacja BetterWorks oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="d0f97-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d0f97-173">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0f97-173">Configure the following claims for this application.</span></span> <span data-ttu-id="d0f97-174">Możesz zarządzać wartości tych atrybutów z "**atrybutu**" aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0f97-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="d0f97-175">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="d0f97-175">The following screenshot shows an example for this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="d0f97-177">Na **atrybuty tokenu SAML** okna dialogowego, dla każdego wiersza w tabeli poniżej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d0f97-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="d0f97-178">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="d0f97-178">Attribute Name</span></span> | <span data-ttu-id="d0f97-179">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="d0f97-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="d0f97-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="d0f97-180">saml_token</span></span>     | <span data-ttu-id="d0f97-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="d0f97-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="d0f97-182">a.</span><span class="sxs-lookup"><span data-stu-id="d0f97-182">a.</span></span> <span data-ttu-id="d0f97-183">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0f97-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="d0f97-186">b.</span><span class="sxs-lookup"><span data-stu-id="d0f97-186">b.</span></span> <span data-ttu-id="d0f97-187">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d0f97-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="d0f97-188">c.</span><span class="sxs-lookup"><span data-stu-id="d0f97-188">c.</span></span> <span data-ttu-id="d0f97-189">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d0f97-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="d0f97-190">d.</span><span class="sxs-lookup"><span data-stu-id="d0f97-190">d.</span></span> <span data-ttu-id="d0f97-191">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-191">Click **Ok**.</span></span>

7. <span data-ttu-id="d0f97-192">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0f97-192">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d0f97-194">Do konfigurowania rejestracji jednokrotnej na **BetterWorks** stronie, musisz wysłać pobrany **XML metadanych** do [BetterWorks obsługuje zespołu](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="d0f97-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="d0f97-195">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="d0f97-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d0f97-196">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="d0f97-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d0f97-197">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0f97-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0f97-198">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f97-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0f97-199">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d0f97-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d0f97-201">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d0f97-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d0f97-202">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d0f97-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0f97-204">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0f97-206">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0f97-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0f97-208">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d0f97-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0f97-210">a.</span><span class="sxs-lookup"><span data-stu-id="d0f97-210">a.</span></span> <span data-ttu-id="d0f97-211">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0f97-212">b.</span><span class="sxs-lookup"><span data-stu-id="d0f97-212">b.</span></span> <span data-ttu-id="d0f97-213">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0f97-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0f97-214">c.</span><span class="sxs-lookup"><span data-stu-id="d0f97-214">c.</span></span> <span data-ttu-id="d0f97-215">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d0f97-216">d.</span><span class="sxs-lookup"><span data-stu-id="d0f97-216">d.</span></span> <span data-ttu-id="d0f97-217">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="d0f97-218">Tworzenie użytkownika testowego BetterWorks</span><span class="sxs-lookup"><span data-stu-id="d0f97-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="d0f97-219">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="d0f97-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="d0f97-220">Praca z [BetterWorks obsługuje zespołu](mailto:support@betterworks.com) Aby dodać użytkowników do platformy BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="d0f97-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d0f97-221">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f97-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d0f97-222">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="d0f97-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d0f97-224">**Aby przypisać Simona Britta BetterWorks, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d0f97-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="d0f97-225">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d0f97-227">Na liście aplikacji zaznacz **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-227">In the applications list, select **BetterWorks**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="d0f97-229">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d0f97-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d0f97-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0f97-231">Click **Add** button.</span></span> <span data-ttu-id="d0f97-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0f97-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d0f97-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d0f97-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d0f97-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0f97-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0f97-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0f97-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0f97-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d0f97-237">Testing single sign-on</span></span>

<span data-ttu-id="d0f97-238">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d0f97-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d0f97-239">Po kliknięciu kafelka BetterWorks w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="d0f97-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0f97-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d0f97-240">Additional resources</span></span>

* [<span data-ttu-id="d0f97-241">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0f97-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0f97-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0f97-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

