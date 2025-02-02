from azure.identity import DefaultAzureCredential
from azure.mgmt.compute import ComputeManagementClient
from azure.mgmt.network import NetworkManagementClient
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.compute.models import (
    HardwareProfile,
    NetworkProfile,
    OsProfile,
    StorageProfile,
    VirtualMachine,
    NetworkInterfaceReference,
    DiskCreateOption,
    CachingTypes,
    OperatingSystemTypes,
    SubResource
)
import subprocess

# Autenticação
credential = DefaultAzureCredential()

# Parâmetros
subscription_id = 'YOUR_SUBSCRIPTION_ID'
resource_group_name = 'YOUR_RESOURCE_GROUP_NAME'
location = 'YOUR_LOCATION'
vm_name = 'YOUR_VM_NAME'
admin_username = 'YOUR_ADMIN_USERNAME'
admin_password = 'YOUR_ADMIN_PASSWORD'
network_interface_id = 'YOUR_NETWORK_INTERFACE_ID'

# Cliente de gestão de recursos
resource_client = ResourceManagementClient(credential, subscription_id)

# Cliente de gestão de rede
network_client = NetworkManagementClient(credential, subscription_id)

# Cliente de gestão de computação
compute_client = ComputeManagementClient(credential, subscription_id)

# Configuração da máquina virtual
vm_parameters = {
    'location': location,
    'hardware_profile': HardwareProfile(vm_size='Standard_DS1_v2'),
    'os_profile': OsProfile(
        computer_name=vm_name,
        admin_username=admin_username,
        admin_password=admin_password
    ),
    'storage_profile': StorageProfile(
        image_reference={
            'publisher': 'Canonical',
            'offer': 'UbuntuServer',
            'sku': '18.04-LTS',
            'version': 'latest'
        },
        'os_disk': {
            'name': f'{vm_name}-osdisk',
            'caching': CachingTypes.READ_WRITE,
            'create_option': DiskCreateOption.FROM_IMAGE,
            'disk_size_gb': 30
        }
    ),
    'network_profile': NetworkProfile(
        network_interfaces=[NetworkInterfaceReference(
            id=network_interface_id,
            primary=True
        )]
    )
}

# Criação da máquina virtual
async_vm_creation = compute_client.virtual_machines.begin_create_or_update(
    resource_group_name,
    vm_name,
    vm_parameters
)
vm_result = async_vm_creation.result()

print(f"Máquina virtual {vm_name} criada com sucesso!")

# Comandos para configurar o acesso RDP
commands = 
