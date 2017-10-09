## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz maszynę Wirtualną z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia. 

Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* i tworzy kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza. toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Podczas tworzenia maszyny Wirtualnej hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład. Zwróć uwagę na powitania `publicIpAddress`. Ten adres jest używany tooaccess hello maszyny Wirtualnej.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a>Otwieranie portu 80 na potrzeby ruchu w sieci Web 

Domyślnie tylko połączeń SSH mają dostęp do maszyn wirtualnych systemu Linux wdrożonych na platformie Azure. Ponieważ ta maszyna wirtualna będzie toobe serwera sieci web, wystarczy tooopen port 80 hello internet. Użyj hello [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port) polecenia tooopen hello żądany port.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>Łączenie z maszyną wirtualną za pośrednictwem protokołu SSH


Jeśli nie znasz już hello publicznego adresu IP maszyny Wirtualnej, uruchom hello [az sieci ip publicznego listy](/cli/azure/network/public-ip#list) polecenia:


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Użyj hello następujące polecenie toocreate jako sesji SSH z maszyną wirtualną hello. Zastąp hello poprawne publiczny adres IP maszyny wirtualnej. W tym przykładzie adres IP hello jest *40.68.254.142*.

```bash
ssh azureuser@40.68.254.142
```

