---
title: "Samouczek: Integracji Azure Active Directory z przedsiębiorstwa znaczeniu Qlik | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Qlik przedsiębiorstwa znaczeniu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4964634cd5aaf0dbb98c766f5e12700c4d118750
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="2bbdb-103">Samouczek: Integracji Azure Active Directory z przedsiębiorstwa znaczeniu Qlik</span><span class="sxs-lookup"><span data-stu-id="2bbdb-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="2bbdb-104">Z tego samouczka dowiesz się sposobu integracji przedsiębiorstwa znaczeniu Qlik z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2bbdb-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2bbdb-105">Integracja z usługą Azure AD przedsiębiorstwa znaczeniu Qlik zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2bbdb-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2bbdb-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Qlik przedsiębiorstwa znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span></span>
- <span data-ttu-id="2bbdb-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do przedsiębiorstwa znaczeniu Qlik (logowanie jednokrotne) z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2bbdb-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2bbdb-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2bbdb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bbdb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2bbdb-110">Prerequisites</span></span>

<span data-ttu-id="2bbdb-111">Aby skonfigurować integrację usługi Azure AD z Qlik przedsiębiorstwa znaczeniu, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2bbdb-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

- <span data-ttu-id="2bbdb-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bbdb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2bbdb-113">Przedsiębiorstwa znaczeniu Qlik logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2bbdb-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2bbdb-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2bbdb-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2bbdb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2bbdb-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2bbdb-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bbdb-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2bbdb-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2bbdb-118">Scenario description</span></span>
<span data-ttu-id="2bbdb-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2bbdb-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2bbdb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2bbdb-121">Dodawanie przedsiębiorstwa znaczeniu Qlik z galerii</span><span class="sxs-lookup"><span data-stu-id="2bbdb-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="2bbdb-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2bbdb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="2bbdb-123">Dodawanie przedsiębiorstwa znaczeniu Qlik z galerii</span><span class="sxs-lookup"><span data-stu-id="2bbdb-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="2bbdb-124">Aby skonfigurować integrację usługi Azure AD Qlik przedsiębiorstwa znaczeniu, należy dodać przedsiębiorstwa znaczeniu Qlik z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2bbdb-125">**Aby dodać przedsiębiorstwa znaczeniu Qlik z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2bbdb-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2bbdb-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="2bbdb-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2bbdb-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="2bbdb-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="2bbdb-133">W polu wyszukiwania wpisz **przedsiębiorstwa znaczeniu Qlik**, wybierz pozycję **przedsiębiorstwa znaczeniu Qlik** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![Przedsiębiorstwa znaczeniu Qlik na liście wyników](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2bbdb-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2bbdb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2bbdb-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Qlik przedsiębiorstwa znaczeniu, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2bbdb-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w przedsiębiorstwie znaczeniu Qlik jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="2bbdb-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w przedsiębiorstwie znaczeniu Qlik musi określone.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="2bbdb-139">W Qlik przedsiębiorstwa znaczeniu, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2bbdb-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Qlik przedsiębiorstwa znaczeniu, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="2bbdb-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2bbdb-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2bbdb-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2bbdb-143">**[Tworzenie użytkownika testowego przedsiębiorstwa znaczeniu Qlik](#create-a-qlik-sense-enterprise-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Qlik znaczeniu przedsiębiorstwo, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2bbdb-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2bbdb-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2bbdb-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2bbdb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2bbdb-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji przedsiębiorstwa znaczeniu Qlik.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="2bbdb-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Qlik przedsiębiorstwa znaczeniu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2bbdb-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="2bbdb-149">W portalu Azure na **przedsiębiorstwa znaczeniu Qlik** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="2bbdb-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="2bbdb-153">Na **adresy URL i domeny przedsiębiorstwa znaczeniu Qlik** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2bbdb-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny przedsiębiorstwa znaczeniu Qlik pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="2bbdb-155">a.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-155">a.</span></span> <span data-ttu-id="2bbdb-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="2bbdb-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2bbdb-157">Należy zwrócić uwagę ukośnika na końcu tego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-157">Note the trailing slash at the end of this URI.</span></span> <span data-ttu-id="2bbdb-158">Jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-158">It is required.</span></span>
    
    <span data-ttu-id="2bbdb-159">b.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-159">b.</span></span> <span data-ttu-id="2bbdb-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="2bbdb-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="2bbdb-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-161">These values are not real.</span></span> <span data-ttu-id="2bbdb-162">Zaktualizować te wartości z rzeczywisty adres URL logowania i identyfikator, które opisano szczegółowo w dalszej części tego samouczka lub skontaktuj się z [zespołem pomocy technicznej klienta przedsiębiorstwa znaczeniu Qlik](https://www.qlik.com/us/services/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-162">Update these values with the actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span></span> 

4. <span data-ttu-id="2bbdb-163">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="2bbdb-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-165">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2bbdb-167">Przygotuj plik XML metadanych Federacji, dzięki czemu można przekazać który serwerowi Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="2bbdb-168">Przed przekazaniem metadanych IdP serwerowi Qlik znaczeniu, plik musi można edytować, aby usunąć informacje, aby zapewnić poprawne działanie między usługą Azure AD i serwer Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="2bbdb-170">a.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-170">a.</span></span> <span data-ttu-id="2bbdb-171">Otwórz plik FederationMetaData.xml, który został pobrany z portalu Azure w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="2bbdb-172">b.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-172">b.</span></span> <span data-ttu-id="2bbdb-173">Wyszukaj wartość **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-173">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="2bbdb-174">Istnieją cztery wpisy (dwie pary otwierające i zamykające znaczniki elementów).</span><span class="sxs-lookup"><span data-stu-id="2bbdb-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="2bbdb-175">c.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-175">c.</span></span> <span data-ttu-id="2bbdb-176">Usuwanie tagów RoleDescriptor i wszystkie informacje między z pliku.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-176">Delete the RoleDescriptor tags and all information in between from the file.</span></span>
   
    <span data-ttu-id="2bbdb-177">d.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-177">d.</span></span> <span data-ttu-id="2bbdb-178">Zapisz plik i zachować w pobliżu do użytku w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-178">Save the file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="2bbdb-179">Przejdź do Qlik znaczeniu Qlik Management Console (QMC) jako użytkownik, który można utworzyć konfiguracji wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="2bbdb-180">W QMC, kliknij polecenie **wirtualnego proxy** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-180">In the QMC, click on the **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="2bbdb-182">W dolnej części ekranu kliknij **Utwórz nowy** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-182">At the bottom of the screen, click the **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="2bbdb-184">Zostanie wyświetlony ekran edycji proxy wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-184">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="2bbdb-185">Po prawej stronie ekranu jest menu do wybierania opcji konfiguracji widoczne.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-185">On the right side of the screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="2bbdb-187">Z zaznaczoną opcją menu identyfikacji wprowadź informacje identyfikujące konfiguracji serwera proxy wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="2bbdb-189">a.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-189">a.</span></span> <span data-ttu-id="2bbdb-190">**Opis** pole jest przyjazną nazwę dla konfiguracji wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-190">The **Description** field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="2bbdb-191">Wprowadź wartość opis.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="2bbdb-192">b.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-192">b.</span></span> <span data-ttu-id="2bbdb-193">**Prefiksu** pole identyfikuje punkt końcowy wirtualnego serwera proxy w celu nawiązania znaczeniu Qlik z usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="2bbdb-194">Wprowadź nazwę unikatowy prefiks dla tego wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="2bbdb-195">c.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-195">c.</span></span> <span data-ttu-id="2bbdb-196">**Limit czasu bezczynności sesji (w minutach)** jest limit czasu dla połączeń za pośrednictwem tego wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="2bbdb-197">d.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-197">d.</span></span> <span data-ttu-id="2bbdb-198">**Nazwy nagłówka pliku cookie sesji** jest nazwą pliku cookie przechowywania identyfikatora sesji dla sesji Qlik znaczeniu, użytkownik otrzymuje po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="2bbdb-199">Ta nazwa musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-199">This name must be unique.</span></span>

12. <span data-ttu-id="2bbdb-200">Kliknij opcję menu uwierzytelniania, aby go wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-200">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="2bbdb-201">Zostanie wyświetlony ekran uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-201">The Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="2bbdb-203">a.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-203">a.</span></span> <span data-ttu-id="2bbdb-204">**Tryb dostępu anonimowego** listy rozwijanej określa użytkowników anonimowych może udostępniać znaczeniu Qlik za pośrednictwem wirtualnej serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="2bbdb-205">Opcją domyślną jest nie użytkownika anonimowego.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-205">The default option is No anonymous user.</span></span>
    
    <span data-ttu-id="2bbdb-206">b.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-206">b.</span></span> <span data-ttu-id="2bbdb-207">**Metodę uwierzytelniania** listy rozwijanej określa użyje schemat uwierzytelniania wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="2bbdb-208">Z listy rozwijanej wybierz SAML.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-208">Select SAML from the drop-down list.</span></span>  <span data-ttu-id="2bbdb-209">W związku z tym pojawi się więcej opcji.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="2bbdb-210">c.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-210">c.</span></span> <span data-ttu-id="2bbdb-211">W **pola identyfikatora URI hosta SAML**, wprowadzania nazwy hosta wprowadzania dostęp znaczeniu Qlik za pośrednictwem tego serwera proxy do wirtualnego SAML.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="2bbdb-212">Nazwa hosta jest identyfikator uri serwera Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-212">The hostname is the uri of the Qlik Sense server.</span></span>
    
    <span data-ttu-id="2bbdb-213">d.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-213">d.</span></span> <span data-ttu-id="2bbdb-214">W **identyfikator jednostki SAML**, wprowadzić tę samą wartość wprowadzona w polu identyfikatora URI hosta SAML.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>
    
    <span data-ttu-id="2bbdb-215">e.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-215">e.</span></span> <span data-ttu-id="2bbdb-216">**Metadanych SAML IdP** jest edytowany wcześniej w pliku **edytowanie metadanych federacji z konfiguracji usługi Azure AD** sekcji.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="2bbdb-217">**Przed przekazaniem metadanych IdP plik musi można edytowane** usunąć informacje, aby zapewnić poprawne działanie między usługą Azure AD i serwer Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="2bbdb-218">**Zapoznaj się instrukcje powyżej, jeśli go jeszcze nie można edytować.**</span><span class="sxs-lookup"><span data-stu-id="2bbdb-218">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="2bbdb-219">Jeśli plik został zmodyfikowany. Kliknij przycisk Przeglądaj i wybierz plik metadanych edytowanych go przekazać do konfiguracji wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>
    
    <span data-ttu-id="2bbdb-220">f.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-220">f.</span></span> <span data-ttu-id="2bbdb-221">Wprowadź odwołanie do atrybutu name lub schemat dla reprezentujący atrybut SAML **UserID** usługi Azure AD, wysyła do serwera Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span></span>  <span data-ttu-id="2bbdb-222">Informacje o odwołaniu schematu jest dostępna w konfiguracji wpisu ekrany aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-222">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="2bbdb-223">Aby użyć atrybutu name, wprowadź `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="2bbdb-224">g.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-224">g.</span></span> <span data-ttu-id="2bbdb-225">Wprowadź wartość dla **katalogu użytkownika** która jest dołączana do użytkowników podczas uwierzytelniania serwera znaczeniu Qlik za pośrednictwem usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="2bbdb-226">Wartości zapisane na stałe muszą być ujęte w **nawiasy kwadratowe []**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="2bbdb-227">Aby użyć atrybutu wysyłane potwierdzenia języka SAML programu Azure AD, wprowadź nazwę atrybutu, w tym polu tekstowym **bez** nawiasy kwadratowe.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="2bbdb-228">h.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-228">h.</span></span> <span data-ttu-id="2bbdb-229">**Algorytm podpisywania SAML** ustawia certyfikatu dostawcy (w tym wielkość server znaczeniu Qlik) usługi podpisywania konfiguracji wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="2bbdb-230">Jeśli serwer znaczeniu Qlik używa zaufanego certyfikatu wygenerowanych przy użyciu Microsoft Enhanced RSA and AES Cryptographic Provider, zmień algorytm podpisywania SAML do **algorytmu SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>
    
    <span data-ttu-id="2bbdb-231">i.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-231">i.</span></span> <span data-ttu-id="2bbdb-232">W sekcji mapowanie atrybutu SAML umożliwia dodatkowych atrybutów, takich jak grupy do wysłania do wykrywania Qlik do użytku w zasadach zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="2bbdb-233">Polecenie **RÓWNOWAŻENIA obciążenia** opcji menu, aby go wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-233">Click on the **LOAD BALANCING** menu option to make it visible.</span></span>  <span data-ttu-id="2bbdb-234">Zostanie wyświetlony ekran równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-234">The Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="2bbdb-236">Polecenie **Dodaj nowy węzeł serwera** przycisku, wybierz aparat węzła lub węzłów znaczeniu Qlik wyśle sesji do celów równoważenia obciążenia, a następnie kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="2bbdb-238">Kliknij opcję menu Zaawansowane, aby go wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-238">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="2bbdb-239">Zostanie wyświetlony ekran Zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-239">The Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="2bbdb-241">Białe listy hostów identyfikuje nazwy hostów, które są akceptowane, gdy połączenie z serwerem Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="2bbdb-242">**Wprowadź nazwę hosta, którego użytkownicy będą wpisywać podczas łączenia z serwerem Qlik znaczeniu.**</span><span class="sxs-lookup"><span data-stu-id="2bbdb-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="2bbdb-243">Nazwa hosta jest taka sama wartość jak identyfikatora uri hosta SAML bez https://.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-243">The hostname is the same value as the SAML host uri without the https://.</span></span>

16. <span data-ttu-id="2bbdb-244">Kliknij przycisk **Zastosuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-244">Click the **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="2bbdb-246">Kliknij przycisk OK, aby zaakceptować komunikat ostrzegawczy z informacją, serwery proxy połączone z wirtualnego serwera proxy zostanie uruchomiona ponownie.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="2bbdb-248">Po prawej stronie ekranu zostanie wyświetlone menu elementy skojarzone.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-248">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="2bbdb-249">Polecenie **proxy** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-249">Click on the **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="2bbdb-251">Zostanie wyświetlony ekran serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-251">The proxy screen appears.</span></span>  <span data-ttu-id="2bbdb-252">Kliknij przycisk **łącze** znajdujący się u dołu do połączenia serwera proxy do wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="2bbdb-254">Wybierz węzeł serwera proxy, który będzie obsługiwać tego połączenia wirtualnego serwera proxy, a następnie kliknij przycisk **łącze** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span></span>  <span data-ttu-id="2bbdb-255">Po połączeniu, serwer proxy, będą wyświetlane w skojarzone serwery proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-255">After linking, the proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="2bbdb-258">Po około pięciu do dziesięciu sekund zostanie wyświetlony komunikat QMC odświeżania.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-258">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="2bbdb-259">Kliknij przycisk **Odśwież QMC** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-259">Click the **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="2bbdb-261">Po odświeżeniu QMC kliknij **proxy wirtualnej** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span></span> <span data-ttu-id="2bbdb-262">Nowy wpis wirtualnego serwera proxy SAML to wymienione w tabeli na ekranie.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-262">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="2bbdb-263">Kliknij wpis wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-263">Single click on the virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="2bbdb-265">W dolnej części ekranu zostanie aktywowany, przycisk Pobierz SP metadanych.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-265">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="2bbdb-266">Kliknij przycisk **SP pobrać metadanych** przycisk, aby zapisać w pliku metadanych.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-266">Click the **Download SP metadata** button to save the metadata to a file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="2bbdb-268">Otwórz plik metadanych sp.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-268">Open the sp metadata file.</span></span>  <span data-ttu-id="2bbdb-269">Obserwować **entityID** wejścia i **AssertionConsumerService** wpisu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="2bbdb-270">Te wartości są równoważne **identyfikator** i **Zaloguj się na adres URL** w konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-270">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="2bbdb-271">Wklej te wartości w **adresy URL i domeny przedsiębiorstwa znaczeniu Qlik** sekcji w konfiguracji aplikacji usługi Azure AD, jeśli ich są niezgodne, a następnie należy zastąpić je w Kreatorze konfiguracji aplikacji Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="2bbdb-273">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="2bbdb-273">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2bbdb-274">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-274">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2bbdb-275">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2bbdb-275">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2bbdb-276">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bbdb-276">Create an Azure AD test user</span></span>
<span data-ttu-id="2bbdb-277">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-277">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="2bbdb-279">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2bbdb-279">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2bbdb-280">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-280">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

   ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2bbdb-282">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-282">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

   !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2bbdb-284">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-284">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

   ![Przycisk Dodaj](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2bbdb-286">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2bbdb-286">In the **User** dialog box, perform the following steps:</span></span>

   ![Okno dialogowe użytkownika](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="2bbdb-288">a.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-288">a.</span></span> <span data-ttu-id="2bbdb-289">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-289">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="2bbdb-290">b.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-290">b.</span></span> <span data-ttu-id="2bbdb-291">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-291">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="2bbdb-292">c.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-292">c.</span></span> <span data-ttu-id="2bbdb-293">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-293">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="2bbdb-294">d.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-294">d.</span></span> <span data-ttu-id="2bbdb-295">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="2bbdb-296">Tworzenie użytkownika testowego przedsiębiorstwa znaczeniu Qlik</span><span class="sxs-lookup"><span data-stu-id="2bbdb-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="2bbdb-297">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Qlik przedsiębiorstwa znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="2bbdb-298">Praca z [zespołem pomocy technicznej klienta przedsiębiorstwa znaczeniu Qlik](https://www.qlik.com/us/services/support) Aby dodać użytkowników na platformie Qlik przedsiębiorstwa znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="2bbdb-299">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2bbdb-300">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bbdb-300">Assign the Azure AD test user</span></span>

<span data-ttu-id="2bbdb-301">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do Qlik przedsiębiorstwa znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-301">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="2bbdb-303">**Aby przypisać Simona Britta Qlik przedsiębiorstwa znaczeniu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2bbdb-303">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="2bbdb-304">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-304">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2bbdb-306">Na liście aplikacji zaznacz **przedsiębiorstwa znaczeniu Qlik**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-306">In the applications list, select **Qlik Sense Enterprise**.</span></span>

    ![Łącze przedsiębiorstwa znaczeniu Qlik na liście aplikacji](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="2bbdb-308">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-308">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="2bbdb-310">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-310">Click **Add** button.</span></span> <span data-ttu-id="2bbdb-311">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="2bbdb-313">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-313">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2bbdb-314">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2bbdb-315">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2bbdb-316">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2bbdb-316">Test single sign-on</span></span>

<span data-ttu-id="2bbdb-317">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-317">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2bbdb-318">Po kliknięciu kafelka Qlik przedsiębiorstwa znaczeniu w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji przedsiębiorstwa znaczeniu Qlik.</span><span class="sxs-lookup"><span data-stu-id="2bbdb-318">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2bbdb-319">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2bbdb-319">Additional resources</span></span>

* [<span data-ttu-id="2bbdb-320">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2bbdb-320">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2bbdb-321">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2bbdb-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

