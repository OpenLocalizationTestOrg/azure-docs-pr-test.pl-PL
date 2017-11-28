## <a name="use-the-azure-portal"></a><span data-ttu-id="d5f89-101">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d5f89-101">Use the Azure portal</span></span>
1. <span data-ttu-id="d5f89-102">Wybierz maszynę Wirtualną, chcesz ponownie wdrożyć, a następnie wybierz *ponownie wdrożyć* przycisk *ustawienia* bloku.</span><span class="sxs-lookup"><span data-stu-id="d5f89-102">Select the VM you wish to redeploy, then select the *Redeploy* button in the *Settings* blade.</span></span> <span data-ttu-id="d5f89-103">Konieczne może być przewiń w dół, aby znaleźć **pomocy technicznej i rozwiązywania problemów** sekcja, która zawiera przycisk "Wdrożenie", jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d5f89-103">You may need to scroll down to see the **Support and Troubleshooting** section that contains the 'Redeploy' button as in the following example:</span></span>
   
    ![Bloku maszyny Wirtualnej platformy Azure](./media/virtual-machines-common-redeploy-to-new-node/vmoverview.png)
2. <span data-ttu-id="d5f89-105">Aby potwierdzić operację, wybierz *ponownie wdrożyć* przycisk:</span><span class="sxs-lookup"><span data-stu-id="d5f89-105">To confirm the operation, select the *Redeploy* button:</span></span>
   
    ![Należy ponownie wdrożyć bloku maszyny Wirtualnej](./media/virtual-machines-common-redeploy-to-new-node/redeployvm.png)
3. <span data-ttu-id="d5f89-107">**Stan** maszyny wirtualnej zmienia się na *aktualizacji* jako maszyna wirtualna przygotowuje się do ponownego wdrażania, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d5f89-107">The **Status** of the VM changes to *Updating* as the VM prepares to redeploy, as shown in the following example:</span></span>
   
    ![Aktualizacja maszyny Wirtualnej](./media/virtual-machines-common-redeploy-to-new-node/vmupdating.png)
4. <span data-ttu-id="d5f89-109">**Stan** zmienia się na *uruchamianie* jako maszyna wirtualna jest uruchamiany na nowy host platformy Azure, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d5f89-109">The **Status** then changes to *Starting* as the VM boots up on a new Azure host, as shown in the following example:</span></span>
   
    ![Uruchamianie maszyny Wirtualnej](./media/virtual-machines-common-redeploy-to-new-node/vmstarting.png)
5. <span data-ttu-id="d5f89-111">Po maszyny Wirtualnej kończy proces rozruchu **stan** następnie wróci do *systemem*, wskazującą maszyna wirtualna ma zostały pomyślnie wdrożone:</span><span class="sxs-lookup"><span data-stu-id="d5f89-111">After the VM finishes the boot process, the **Status** then returns to *Running*, indicating the VM has been successfully redeployed:</span></span>
   
    ![Uruchamianie maszyny Wirtualnej](./media/virtual-machines-common-redeploy-to-new-node/vmrunning.png)

