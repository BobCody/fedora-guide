# FEDORA guide

## добавляем репозитории 

Чтобы включить как бесплатные, так и несвободные репозитории RPM Fusion в вашей системе Fedora, запустите:

```sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm```

## настройка видеокарты

смотрим драйвер: 

```lspci -k | grep -EA3 'VGA|3D|Display'```

устанавливаем amdgpu:

```sudo dnf install xorg-x11-drv-amdgpu mesa-vulkan-drivers.x86_64 mesa-vulkan-drivers.i686 vulkan-loader.x86_64 vulkan-loader.i686 vulkan-tools```

если будет запускаться Wine:

```sudo dnf install wine-dxvk.x86_64 wine-dxvk.i686```

добавлем строки в grub:

```sudo geany /etc/default/grub```

For Southern Island cards (моя): 

```radeon.si_support=0 amdgpu.si_support=1```

For Sea Island cards: 

```radeon.cik_support=0 amdgpu.cik_support=1```

обновляем grub

```sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg```

## Soft

### Timeshift

установим последнюю версию программы Timeshift. Добавим пользовательский репозиторий copr:

```sudo dnf copr enable oprizal/timeshift-upstream```

обновить загрузчик

```sudo grub2-mkconfig -o /boot/grub2/grub.cfg```