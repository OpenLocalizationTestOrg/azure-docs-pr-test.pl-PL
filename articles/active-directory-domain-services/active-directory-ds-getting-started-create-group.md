---
title: "Azure Active Directory Domain Services: Utwórz grupę Administratorzy kontrolerów domeny usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Włączanie usług Azure Active Directory Domain Services przy użyciu klasycznej witryny Azure Portal"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="ae23d-103">Włączanie usług Azure Active Directory Domain Services przy użyciu klasycznej witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ae23d-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>
<span data-ttu-id="ae23d-104">W tym artykule opisano i przedstawiono zadania konfiguracji, które są wymagane, aby włączyć usługi Azure Active Directory Domain Services (Azure AD DS) dla dzierżawy usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae23d-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="ae23d-105">[**Zamiast tego spróbuj nowe środowisko portalu Azure (wersja zapoznawcza)**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="ae23d-105">[**Try the new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a><span data-ttu-id="ae23d-106">Zadanie 1: Tworzenie grupy administratorów usługi Azure AD kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="ae23d-106">Task 1: create the Azure AD DC administrators group</span></span>
<span data-ttu-id="ae23d-107">Pierwszym zadaniem jest tworzenie grupy administracyjnej w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae23d-107">The first task is to create an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="ae23d-108">Nosi nazwę tej grupy administracyjnej specjalne *Administratorzy kontrolera domeny usługi AAD*.</span><span class="sxs-lookup"><span data-stu-id="ae23d-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="ae23d-109">Członkowie tej grupy są przyznawane uprawnienia administracyjne na komputerach, które są przyłączone do domeny w domenie zarządzanych usług domenowych Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae23d-109">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="ae23d-110">Na komputerach przyłączonych do domeny ta grupa jest dodawane do grupy Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="ae23d-110">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="ae23d-111">Ponadto Członkowie tej grupy służy pulpitu zdalnego do łączności zdalnej dla komputerów przyłączonych do domeny.</span><span class="sxs-lookup"><span data-stu-id="ae23d-111">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="ae23d-112">Nie masz uprawnienia administratora domeny lub administratora przedsiębiorstwa domeny zarządzanej, który został utworzony za pomocą usługi Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="ae23d-112">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="ae23d-113">W domenach zarządzanych te uprawnienia są zastrzeżone przez usługę i nie są udostępniane użytkownikom w ramach dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="ae23d-113">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="ae23d-114">Jednak można użyć specjalnej grupy administracyjne utworzone w ramach tego zadania konfiguracji można wykonać pewne operacje uprzywilejowane.</span><span class="sxs-lookup"><span data-stu-id="ae23d-114">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="ae23d-115">Tych operacji zalicza się przyłączanie komputerów do domeny, należą do tej grupy administracyjnej na komputerach przyłączonych do domeny i konfigurowania zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="ae23d-115">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="ae23d-116">W tym zadaniu konfiguracji tworzenia grupy administracyjnej i Dodaj jeden lub więcej użytkowników w katalogu do grupy.</span><span class="sxs-lookup"><span data-stu-id="ae23d-116">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span></span> <span data-ttu-id="ae23d-117">Aby utworzyć grupy administracyjnej dla usługi Azure Active Directory Domain Services, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ae23d-117">To create the administrative group for Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="ae23d-118">Przejdź do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ae23d-118">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ae23d-119">W lewym okienku wybierz przycisk **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae23d-119">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="ae23d-120">Wybierz dzierżawę usługi Azure AD (katalog), dla którego chcesz włączyć usługi Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="ae23d-120">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="ae23d-121">Można utworzyć tylko jedną domenę dla każdego katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae23d-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Wybierz katalog usługi Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="ae23d-123">Na **katalogu podglądu** kliknij przycisk **grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="ae23d-123">On the **preview directory** page, click the **Groups** tab.</span></span>
5. <span data-ttu-id="ae23d-124">Aby dodać grupę do dzierżawy usługi Azure AD, w okienku zadań w dolnej części okna kliknij **Dodaj grupę**.</span><span class="sxs-lookup"><span data-stu-id="ae23d-124">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span></span>

    ![Przycisk Dodaj grupę](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="ae23d-126">W **Dodaj grupę** okna dialogowego Utwórz grupę o nazwie **Administratorzy kontrolera domeny usługi AAD**, a następnie ustaw **typ grupy** do **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="ae23d-126">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="ae23d-127">Aby włączyć dostęp w swojej domenie zarządzanych usług domenowych Azure Active Directory, należy utworzyć grupę o tej nazwie dokładne.</span><span class="sxs-lookup"><span data-stu-id="ae23d-127">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![Okno dialogowe Dodawanie grupy](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="ae23d-129">W **opis** wprowadź opis, który umożliwia użytkownikom zrozumienie, że ta grupa przyznaje uprawnienia administracyjne w ramach usług domenowych Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae23d-129">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="ae23d-130">Po utworzeniu grupy, kliknij nazwę grupy, aby wyświetlić jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="ae23d-130">After you've created the group, click the group name to view its properties.</span></span>
9. <span data-ttu-id="ae23d-131">Aby dodać użytkowników jako członków grupy, w dolnej części okna kliknij pozycję **Dodaj członków** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ae23d-131">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span></span>

    ![Dodawanie przycisku członków grupy](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="ae23d-133">W **dodawać członków** oknie dialogowym Wybierz użytkowników, którzy powinny być członkami tej grupy, a następnie kliknij ikonę znacznika wyboru w prawej dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="ae23d-133">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span></span>

    ![Dodawanie użytkowników do grupy administratorów](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="ae23d-135">Następny krok</span><span class="sxs-lookup"><span data-stu-id="ae23d-135">Next step</span></span>
[<span data-ttu-id="ae23d-136">Zadanie 2: Tworzenie lub Wybieranie sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ae23d-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
