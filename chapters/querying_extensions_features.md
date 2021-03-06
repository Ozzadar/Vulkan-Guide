# Querying Properties, Extensions, Features, Limits, and Formats

One of Vulkan's main features is that is can be used to develop on multiple platforms and devices. To make this possible, an application is responsible for querying the information from each physical device and then basing decisions on this information.

The items that can be queried from a physical device

- Properties
- Features
- Extensions
- Limits
- Formats

## Properties

There are many other components in Vulkan that are labeled as properties. The term "properties" is an umbrella term for any read-only data that can be queried.

## Extensions

> Check out the [Enabling Extensions](./enabling_extensions.md) chapter for more information.
>
> There is a [Registry](https://www.khronos.org/registry/vulkan/#repo-docs) with all available extensions.

There are many times when a set of new functionality is desired in Vulkan that doesn't currently exist. Extensions have the ability to add new functionality. Extensions may define new Vulkan functions, enums, structs, or feature bits. While all of these extended items are found by default in the Vulkan Headers, it is **undefined behavior** to use extended Vulkan if the [extensions are not enabled](./enabling_extensions.md).

## Features

> Checkout the [Enabling Features](./enabling_features.md) chapter for more information.

Features describe functionality which is not supported on all implementations. Features can be [queried](https://www.khronos.org/registry/vulkan/specs/1.2/html/vkspec.html#vkGetPhysicalDeviceFeatures) and then enabled when creating the `VkDevice`. Besides the [list of all features](https://www.khronos.org/registry/vulkan/specs/1.2/html/vkspec.html#features), some [features are mandatory](https://www.khronos.org/registry/vulkan/specs/1.2-extensions/html/vkspec.html#features-requirements) due to newer Vulkan versions or use of extensions.

A common technique is for an extension to expose a new struct that can be passed through `pNext` that adds more features to be queried.

## Limits

Limits are implementation-dependent minimums, maximums, and other device characteristics that an application may need to be aware of. Besides the [list of all limits](https://www.khronos.org/registry/vulkan/specs/1.2/html/vkspec.html#limits), some limits also have [minimum/maximum required values](https://www.khronos.org/registry/vulkan/specs/1.2/html/vkspec.html#limits-minmax) guaranteed from a Vulkan implementation.

## Formats

Every `VkBuffer` and `VkImage` requires a format from the supported Vulkan [VkFormat](https://www.khronos.org/registry/vulkan/specs/1.2/html/vkspec.html#formats-definition) list. The supported formats may vary across implementations, but a [minimum set of format features are guaranteed](https://www.khronos.org/registry/vulkan/specs/1.2/html/vkspec.html#features-required-format-support). An application can [query](https://www.khronos.org/registry/vulkan/specs/1.2/html/vkspec.html#formats-properties) for the supported format properties.

Each format has a set of `VkFormatFeatureFlagBits` for how the format is supported or not. These features bits are grouped further for how the format is used.

> Example: One can check if the `VK_FORMAT_R8_UNORM` format supports being sampled when an images is created with a `tiling` parameter of `VK_IMAGE_TILING_LINEAR`.
>
> To do this, query the `linearTilingFeatures` flags for `VK_FORMAT_R8_UNORM` to see if the `VK_FORMAT_FEATURE_SAMPLED_IMAGE_BIT` is set for the implementation.

### External Formats

Currently only supported with the `VK_ANDROID_external_memory_android_hardware_buffer` extension. This extension allows Android applications to import implementation-defined external formats. There are many restrictions what are allowed with these external formats which are [documented in the spec.](https://www.khronos.org/registry/vulkan/specs/1.2-extensions/html/vkspec.html#memory-external-android-hardware-buffer-external-formats)

## Tools

There are a few tools to help with getting all the information in a quick and in a human readable format.

`vulkaninfo` is a command line utility for Windows, Linux, and macOS that enables you to see all the available items listed above about your GPU. Refer to the [Vulkaninfo documentation](https://vulkan.lunarg.com/doc/sdk/latest/windows/vulkaninfo.html) in the Vulkan SDK.

The [Vulkan Hardware Capability Viewer](https://play.google.com/store/apps/details?id=de.saschawillems.vulkancapsviewer&hl=en_US) app developed by Sascha Willems, is an Android app to display all details for devices that support Vulkan.
