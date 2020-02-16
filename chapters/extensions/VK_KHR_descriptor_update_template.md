# VK_KHR_descriptor_update_template

> Promoted to core in Vulkan 1.1

This extension is designed around how some applications create and update many `VkDescriptorSets` during the initialization phase. It's not unlikely that a lot of updates end up having the same `VkDescriptorLayout` and the same bindings are being updated so therefore descriptor update templates are designed to only pass the update information once.

The descriptors themselves are not specified in the `VkDescriptorUpdateTemplate`, rather, offsets into an application provided pointer to host memory are specified, which are combined with a pointer passed to `vkUpdateDescriptorSetWithTemplate` or `vkCmdPushDescriptorSetWithTemplateKHR`. This allows large batches of updates to be executed without having to convert application data structures into a strictly-defined Vulkan data structure.