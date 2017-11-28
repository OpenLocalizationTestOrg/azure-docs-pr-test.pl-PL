---
title: 'Samouczek: Integracji Azure Active Directory z iLMS | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 22c72020200138e78835ed7dd2661f18b824c785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="c5b1c-103">Samouczek: Integracji Azure Active Directory z iLMS</span><span class="sxs-lookup"><span data-stu-id="c5b1c-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="c5b1c-104">Z tego samouczka dowiesz się integrowanie iLMS z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5b1c-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5b1c-105">Integracja z usługą Azure AD iLMS zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c5b1c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do iLMS</span><span class="sxs-lookup"><span data-stu-id="c5b1c-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="c5b1c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do iLMS (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b1c-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5b1c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c5b1c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c5b1c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5b1c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5b1c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c5b1c-110">Prerequisites</span></span>

<span data-ttu-id="c5b1c-111">Aby skonfigurować integrację usługi Azure AD z iLMS, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="c5b1c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b1c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5b1c-113">ILMS jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c5b1c-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5b1c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5b1c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5b1c-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c5b1c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5b1c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5b1c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c5b1c-118">Scenario description</span></span>
<span data-ttu-id="c5b1c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5b1c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5b1c-121">Dodawanie iLMS z galerii</span><span class="sxs-lookup"><span data-stu-id="c5b1c-121">Adding iLMS from the gallery</span></span>
2. <span data-ttu-id="c5b1c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c5b1c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="c5b1c-123">Dodawanie iLMS z galerii</span><span class="sxs-lookup"><span data-stu-id="c5b1c-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="c5b1c-124">Aby skonfigurować integrację usługi Azure AD iLMS, należy dodać iLMS z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c5b1c-125">**Aby dodać iLMS z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c5b1c-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c5b1c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c5b1c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c5b1c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c5b1c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c5b1c-133">W polu wyszukiwania wpisz **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-133">In the search box, type **iLMS**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="c5b1c-135">W panelu wyników wybierz **iLMS**, następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5b1c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c5b1c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5b1c-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z iLMS w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5b1c-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w iLMS jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="c5b1c-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w iLMS musi się.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="c5b1c-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w iLMS.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="c5b1c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z iLMS, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c5b1c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c5b1c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5b1c-145">**[Tworzenie użytkownika testowego iLMS](#creating-an-ilms-test-user)**  — mają odpowiednika Simona Britta w iLMS połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c5b1c-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5b1c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5b1c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c5b1c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5b1c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji iLMS.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="c5b1c-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z iLMS, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c5b1c-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="c5b1c-151">W portalu Azure na **iLMS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c5b1c-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="c5b1c-155">Na **iLMS domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="c5b1c-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-157">a.</span></span> <span data-ttu-id="c5b1c-158">W **identyfikator** pole tekstowe, Wklej **identyfikator** wartość skopiować z **usługodawcy** sekcji SAML ustawień w portalu administracyjnym iLMS.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="c5b1c-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-159">b.</span></span> <span data-ttu-id="c5b1c-160">W **adres URL odpowiedzi** pole tekstowe, Wklej **(adres URL punktu końcowego)** wartość skopiować z **usługodawcy** sekcji SAML ustawień w portalu administratora iLMS o następującego wzorca`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="c5b1c-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="c5b1c-161">Ta 123456 jest Przykładowa wartość identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="c5b1c-162">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="c5b1c-164">W **adres URL logowania** pole tekstowe, Wklej **(adres URL punktu końcowego)** wartość skopiować z **usługodawcy** sekcji SAML ustawień w portalu administracyjnym iLMS jako`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="c5b1c-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="c5b1c-165">Aby włączyć JIT inicjowania obsługi administracyjnej, iLMS aplikacji oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c5b1c-166">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-166">Configure the following claims for this application.</span></span> <span data-ttu-id="c5b1c-167">Możesz zarządzać wartości tych atrybutów z **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="c5b1c-168">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-168">The following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="c5b1c-170">Utwórz **działu, Region** i **dzielenia** atrybutów, a następnie dodaj nazwę tych atrybutów w iLMS.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="c5b1c-171">Te atrybuty pokazanym powyżej są wymagane.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="c5b1c-172">Należy włączyć **Utwórz konto użytkownika Un-recognized** w iLMS mapować te atrybuty.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="c5b1c-173">Postępuj zgodnie z instrukcjami [tutaj](http://support.inspiredelearning.com/customer/portal/articles/2204526) Aby poznać konfiguracji atrybutów.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

6. <span data-ttu-id="c5b1c-174">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="c5b1c-175">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="c5b1c-175">Attribute Name</span></span> | <span data-ttu-id="c5b1c-176">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="c5b1c-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="c5b1c-177">dzielenie</span><span class="sxs-lookup"><span data-stu-id="c5b1c-177">division</span></span> | <span data-ttu-id="c5b1c-178">User.Department</span><span class="sxs-lookup"><span data-stu-id="c5b1c-178">user.department</span></span> |
    | <span data-ttu-id="c5b1c-179">Region</span><span class="sxs-lookup"><span data-stu-id="c5b1c-179">region</span></span> | <span data-ttu-id="c5b1c-180">User.state</span><span class="sxs-lookup"><span data-stu-id="c5b1c-180">user.state</span></span> |
    | <span data-ttu-id="c5b1c-181">Dział</span><span class="sxs-lookup"><span data-stu-id="c5b1c-181">department</span></span> | <span data-ttu-id="c5b1c-182">User.jobtitle</span><span class="sxs-lookup"><span data-stu-id="c5b1c-182">user.jobtitle</span></span> |

    <span data-ttu-id="c5b1c-183">a.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-183">a.</span></span> <span data-ttu-id="c5b1c-184">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="c5b1c-187">b.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-187">b.</span></span> <span data-ttu-id="c5b1c-188">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c5b1c-189">c.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-189">c.</span></span> <span data-ttu-id="c5b1c-190">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c5b1c-191">d.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-191">d.</span></span> <span data-ttu-id="c5b1c-192">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="c5b1c-192">Click **Ok**</span></span>

7. <span data-ttu-id="c5b1c-193">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="c5b1c-195">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-195">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="c5b1c-197">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **portalu administracyjnego iLMS** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="c5b1c-198">Kliknij przycisk **SSO:SAML** w obszarze **ustawienia** kartę, aby otworzyć ustawienia SAML i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="c5b1c-200">a.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-200">a.</span></span> <span data-ttu-id="c5b1c-201">Rozwiń węzeł **usługodawcy** sekcji i skopiuj **identyfikator** i **(adres URL punktu końcowego)** wartość.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="c5b1c-203">b.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-203">b.</span></span> <span data-ttu-id="c5b1c-204">W obszarze **dostawcy tożsamości** kliknij **Importowanie metadanych**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="c5b1c-205">c.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-205">c.</span></span> <span data-ttu-id="c5b1c-206">Wybierz **metadanych** plik pobrany z portalu Azure z **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="c5b1c-208">d.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-208">d.</span></span> <span data-ttu-id="c5b1c-209">Jeśli chcesz włączyć JIT inicjowania obsługi administracyjnej na tworzenie kont iLMS dla un-rozpoznaje użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="c5b1c-210">Sprawdź **utworzyć konto użytkownika nie jest rozpoznawaną**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="c5b1c-212">Mapowanie atrybutów w usłudze Azure AD z atrybutów w iLMS.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-212">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="c5b1c-213">W kolumnie atrybutów Określ nazwę atrybuty lub wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-213">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="c5b1c-214">e.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-214">e.</span></span> <span data-ttu-id="c5b1c-215">Przejdź do **reguły biznesowe** karcie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-215">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="c5b1c-217">Sprawdź **Tworzenie regionów Un-recognized, działów i działów** do tworzenia regionów, działów i działów, które jeszcze nie istnieją w czasie rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-217">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="c5b1c-218">Sprawdź **aktualizacji użytkownika profilu podczas logowania** do określenia, czy profil użytkownika jest aktualizowany przy każdej rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-218">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="c5b1c-219">Jeśli **"Aktualizacji puste wartości dla innych niż obowiązkowego pola w profilu użytkownika"** opcja jest zaznaczona, profil opcjonalne pola, które są puste podczas logowania zostanie także spowodować profilu użytkownika iLMS zawiera puste wartości dla tych pól.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-219">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="c5b1c-220">Sprawdź **Wyślij E-mail z powiadomieniem błąd** , a następnie wprowadź adres e-mail użytkownika, których chcesz otrzymywać wiadomość e-mail z powiadomieniem błąd.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-220">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

11. <span data-ttu-id="c5b1c-221">Kliknij przycisk **zapisać** przycisk, aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-221">Click **Save** button to save the settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="c5b1c-223">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c5b1c-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c5b1c-224">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c5b1c-225">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5b1c-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5b1c-226">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b1c-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5b1c-227">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c5b1c-229">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c5b1c-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c5b1c-230">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5b1c-232">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-232">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5b1c-234">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-234">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5b1c-236">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5b1c-238">a.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-238">a.</span></span> <span data-ttu-id="c5b1c-239">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5b1c-240">b.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-240">b.</span></span> <span data-ttu-id="c5b1c-241">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5b1c-242">c.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-242">c.</span></span> <span data-ttu-id="c5b1c-243">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c5b1c-244">d.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-244">d.</span></span> <span data-ttu-id="c5b1c-245">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="c5b1c-246">Tworzenie użytkownika testowego iLMS</span><span class="sxs-lookup"><span data-stu-id="c5b1c-246">Creating an iLMS test user</span></span>

<span data-ttu-id="c5b1c-247">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-247">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="c5b1c-248">JIT będzie działać, jeśli kliknięto **Utwórz konto użytkownika Un-recognized** wyboru podczas SAML ustawienie konfiguracji w portalu administracyjnym iLMS.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-248">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="c5b1c-249">Jeśli trzeba ręcznie utworzyć użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c5b1c-249">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="c5b1c-250">Zaloguj się do witryny firmy iLMS jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-250">Log in to your iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="c5b1c-251">Kliknij przycisk **"Zarejestruj użytkownika"** w obszarze **użytkowników** kartę, aby otworzyć **zarejestrować użytkownika** strony.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-251">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![Dodawanie pracownika](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="c5b1c-253">Na **"Zarejestruj użytkownika"** wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-253">On the **“Register User”** page, perform the following steps.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="c5b1c-255">a.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-255">a.</span></span> <span data-ttu-id="c5b1c-256">W **imię** pole tekstowe, nazwa typu pierwszy Britta.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-256">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="c5b1c-257">b.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-257">b.</span></span> <span data-ttu-id="c5b1c-258">W **nazwisko** tekstowym, wpisz nazwisko Simona.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-258">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="c5b1c-259">c.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-259">c.</span></span> <span data-ttu-id="c5b1c-260">W **identyfikator wiadomości E-mail** tekstowym, wpisz adres e-mail konta Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-260">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="c5b1c-261">d.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-261">d.</span></span> <span data-ttu-id="c5b1c-262">W **Region** listy rozwijanej wybierz wartość dla regionu.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-262">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="c5b1c-263">e.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-263">e.</span></span> <span data-ttu-id="c5b1c-264">W **dzielenia** listy rozwijanej wybierz wartość dla działu.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-264">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="c5b1c-265">f.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-265">f.</span></span> <span data-ttu-id="c5b1c-266">W **działu** listy rozwijanej wybierz wartość dla działu.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-266">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="c5b1c-267">g.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-267">g.</span></span> <span data-ttu-id="c5b1c-268">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5b1c-269">Wiadomość e-mail rejestracji można wysłać do użytkownika, wybierając **wysłać wiadomość E-mail rejestracji** wyboru.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-269">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c5b1c-270">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b1c-270">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c5b1c-271">W tej sekcji można włączyć Simona Britta do udostępnienia jej iLMS za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-271">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c5b1c-273">**Aby przypisać Simona Britta iLMS, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c5b1c-273">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="c5b1c-274">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-274">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c5b1c-276">Na liście aplikacji zaznacz **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-276">In the applications list, select **iLMS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="c5b1c-278">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-278">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c5b1c-280">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-280">Click **Add** button.</span></span> <span data-ttu-id="c5b1c-281">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c5b1c-283">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-283">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c5b1c-284">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5b1c-285">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5b1c-286">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c5b1c-286">Testing single sign-on</span></span>

<span data-ttu-id="c5b1c-287">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c5b1c-288">Po kliknięciu kafelka iLMS w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji iLMS.</span><span class="sxs-lookup"><span data-stu-id="c5b1c-288">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5b1c-289">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c5b1c-289">Additional resources</span></span>

* [<span data-ttu-id="c5b1c-290">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5b1c-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5b1c-291">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5b1c-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

