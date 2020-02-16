# Device Groups

> Promoted to core in Vulkan 1.1

Device groups are a way to have multiple physical devices (single-vendor) represented as a single logical device. If for example you have two of the same GPU, connected by some vendor provided bridge interface, in a single system, one approuch is to create two logical devices in Vulkan. The issue here is that there are limitations what can be shared and synchronized between two `VkDevice` objects which is not a bad thing, but there are use cases where an application might want to combine the memory between two GPUs. Device Groups were designed for this use case by having you create "sub-devices" to a single `VkDevice`.

With device groups, objects like `VkCommandBuffers` and `VkQueue` are not tied to a single "sub-device" but instead the driver will manage which physical device to run it on. Another usage of device group is alternative frame presenting where every frame is displayed by a different "sub-device". When it comes to memory scope, a new `DeviceGroup` memory scope was created which defines when memory is visable and avaiable between each "sub-device"

There are two extensions, `VK_KHR_device_group` and `VK_KHR_device_group_creation`. The reason for two seperate extensions is that extensions are either "instance level extensions" or "device level extensions". Since device groups need to interact with instance level calls as well as device level calls, two extensions were created.