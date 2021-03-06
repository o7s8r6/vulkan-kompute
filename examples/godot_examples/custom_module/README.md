# Vulkan Kompute Godot Example

![](https://github.com/EthicalML/vulkan-kompute/raw/master/docs/images/komputer-godot-4.gif)

## Set Up Dependencies

### Vulkan

You will need the Vulkan SDK, in this case we use version `1.2.148.1`, which you can get at the official site https://vulkan.lunarg.com/sdk/home#windows

This will have the following contents that will be required later on:

* The VulkanSDK static library `vulkan-1`

### Kompute

We will be using v0.3.1 of Kompute, and similar to above we will need the built static library, but in this case we will build it.

We can start by cloning the repository on the v0.3.1 branch:

```
git clone --branch v0.3.1 https://github.com/EthicalML/vulkan-kompute/
```

You will be able to use cmake to generate the build files for your platform.

```
cmake vulkan-kompute/. -Bvulkan-kompute/build
```

You need to make sure that the build is configured with the same flags required for godot, for example, in windows you will need:

* Release build
* Configuration type: static library
* Runtime lib: Multi-threaded / multi-threaded debug

Now you should see the library built under `build/src/Release`

## Building Godot

Now to build godot you will need to set up a couple of things for the Scons file to work - namely setting up the following:

* Copy the `vulkan-1` library from your vulkan sdk folder to `lib/vulkan-1.lib`
* Copy the `kompute.lib` library from the Kompute build to `lib/kompute.lib`
* Copy the `include/vulkan/` folder to the `./include/` folder
* Copy the `single_include/kompute/` to the `./include/` folder
* Make sure the versions above match as we provide the headers in the `include` folder - if you used different versions make sure these match as well

### Clone godot repository

Now we can clone the godot repository - it must be on a separate repository, so you can use the parent directory if you are on the Kompute repo.

```
cd ../../godot_engine

git clone --branch 3.2.3-stable https://github.com/godotengine/godot

cd godot/
```

And now we can build against our module

```
wscons -j16 custom_modules=../../custom_module/ platform=windows target=release_debug
```

Once we have built it we can now run the generated godot engine in the `bin/` folder, and we will be able to access the custom module from anywhere in the project, as well as creating new nodes from the user interface.



